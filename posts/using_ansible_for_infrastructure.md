# Using Ansible for infrastructure

For the last year or so, the majority of our new projects at MadeTech, have used Ansible as our go-to tool for provisioning and configuring our servers with the software that runs on them. We've paired Terraform with Ansible and Chef previously for creating our cloud resources, but have recently been experimenting with using Ansible to see if the one tool was capable of both of these stages in our infrastructure setups. We've not been disappointed with our experiences so far.

## Ansible and Amazon Web Services

Ansible has support for a variety of cloud services out of the box with the more recent releases. To name a few, AWS, Azure, Google and Rackspace. Full support of each of the services API's varies, however it appears as though AWS has the most supported set of features by Ansible.

If you're familiar with using Ansible for provisioning your servers, then creating resources in the cloud is almost identical. You use AWS specific modules that represent the resources in AWS, and once defined in YAML, you're apply to run an Ansible playbook to apply those resources to your AWS account.

## AWS credentials

When using Ansible with AWS, when you run your playbook - Ansible will be running commands from your local machine using the AWS API. It uses a Python library behind the scenes called boto to do this. As with most AWS libraries, boto looks for a configuration file on your computer located at `~/.aws/credentials`. In this file I find it useful to group credentials into separate profiles so that you can be explicit in which credentials to use when running a command. For example, your credentials file may look like:

```ini
[playground]
aws_access_key_id = 13ABCHHASDBYB2U3NG34NG
aws_secret_access_key = nfu8n3787N4F874GN8n7g847878G87NG/GUNREIN
```

I'd be able to use these credentials by specifiying the profile `playground` in my commands.

## Infrastructure playbook

When setting up new resources for an infrastructure project, the first thing I usually do is setup the SSH keys that we'll be using in future to connect to any servers to provision them. I create an SSH on my machine, and then add it to AWS.

To generate the key I use:

```
ssh-keygen -t rsa -C web -f ./web -P ''
```

The value for the `-C` flag is the comment that is included in the public key. This can be something descriptive related to the project you're working on. The `-f` value is the name of the file that the keypair will be saved to. The value you specify will be the exact name for the private key. The public key will have a `.pub` appended onto the filename automatically.

Create another file called `build-infra.yml` and in this file include:

```yml
---
- hosts: localhost
  connection: local
  gather_facts: false

  tasks:
    - name: Add web keypair
      ec2_key:
        name: web
        key_material: "{{ lookup('file', 'web.pub') }}"
        state: present
```

The first three options, `hosts`, `connection` and `gather_facts` are setting up the Ansible playbook to use your local machine to run the subsequent modules that we define in it. As mentioned above, that is because behind the scenes we use our local computer to do the communication with the AWS API.

We're then defining a standard Ansible task using one of the AWS modules, in this case, `ec2_key` which is used for managing AWS security keys. We tell AWS to use the name `web` for the key, and to load the content from the local file `web.pub` as the key content in AWS.

To run this, we use the following command:

```
AWS_PROFILE=playground AWS_REGION=eu-west-1 ansible-playbook build-infra.yml
```

We prefix the standard `ansible-playbook` command with two environment variables that are used behind the scenes by the boto library to connect to the AWS library. We tell it to use the `playground` profile from our `~/.aws/credentials` file to connect to the API, and to run the AWS operations within the `eu-west-1` AWS region.

By building our AWS playbooks in this manner, it makes them far more reusable than if we were to hardcode these values directly into our playbooks.

## Lack of state file

Running the above command, you should see some output with a `[changed]` value next to the `Add web keypair` task. Run the command again, and the same task will have an `[ok]` flag next to it as nothing has changed.

I see this as one of the benefits to using Ansible compared to Terraform. Ansible will check for state directly with AWS rather than a local state file that is updated each time a command is run.

## Using resources between tasks

Some of the AWS Ansible modules require you to reference other AWS resources that you have created. You can use Ansible variables to manage these. To better demonstrate this, lets build the following resources; a set of three EC2 instances with Elastic IP addresses associated to them, that are sitting behind an Elastic Load Balancer. We'll setup a security group and assign the instances to these, and then attach each instance to the load balancer.

 1. Create keypair for instances (already done above)
 2. Create a security group to assign instances to
 3. Create three instances
 4. Assign Elastic IP addresses to instances
 5. Create a security group for the load balancer
 6. Create a load balancer
 7. Assign instances to load balancer

For each of the above steps, we'll add the following tasks to our YAML file:

```yml
- name: Add web instances security group
  ec2_group:
    name: web_instances
    description: Web instances
    rules_egress:
      - proto: -1
        from_port: -1
        to_port: -1
        cidr_ip: 0.0.0.0/0
    rules:
      - proto: tcp
        from_port: 22
        to_port: 22
        cidr_ip: 0.0.0.0/0
      - proto: tcp
        from_port: 80
        to_port: 80
        cidr_ip: 0.0.0.0/0
```

This is a standard security group permitting all outgoing traffic from the instances, and only allowing SSH and HTTP access inbound.

```yml
- name: Provision web instances
  ec2:
    key_name: web
    group: web_instances
    instance_type: t2.small
    image: ami-a192bad2
    wait: true
    exact_count: 3
    count_tag:
      Name: web
    instance_tags:
      Name: web
  register: web_instances
```

The `ec2` module creates, modifies and removes EC2 instances based on the count of instances that are present with a particular tag assigned to them. In this case, we will create the number of EC2 instances defined by the `exact_count` value that have the `Name` tag of `web` assigned to them.

We store the details of these instances in a variable called `web_instances` once the command has completed. We'll then use this variable to assign Elastic IP addresses to them in the following command:

```yml
- name: Assign EIP address for web instances
  ec2_eip:
    device_id: "{{ item.id }}"
    in_vpc: true
    release_on_disassociation: true
  with_items: "{{ web_instances.tagged_instances }}"
```

In the above Ansible module, we're using the `with_items` option to loop over a variable and run the `ec2_eip` module on each value. The `ec2_eip` module will allocate an EIP and associate it to the instance specified by the `device_id` value.

```yml
- name: Add load balancer security group
  ec2_group:
    name: web_load_balancer
    description: Web load balancer
    rules_egress:
      - proto: -1
        from_port: -1
        to_port: -1
        cidr_ip: 0.0.0.0/0
    rules:
      - proto: tcp
        from_port: 80
        to_port: 80
        cidr_ip: 0.0.0.0/0
```

Similar to our instance security group, we create another that will be associated to the load balancer. Again we permit all outgoing traffic, but restrict access to HTTP only. For the specific instances, we'll connect directly to them over SSH, therefore this protocol doesn't need to be enabled on this group.

```yml
- name: Setup web load balancer
  ec2_elb_lb:
    name: web
    state: present
    idle_timeout: 300
    zones:
      - eu-west-1a
    listeners:
      - protocol: http
        load_balancer_port: 80
        instance_port: 80
    security_group_names:
      - web_load_balancer
  register: web_load_balancer
```

The above creates our load balancer with our specified security group. We listen for traffic on HTTP port 80 only.

```yml
- name: Add web instances to load balancer
  ec2_elb:
    instance_id: "{{ item.id }}"
    ec2_elbs: web
    state: present
    wait: false
  when: item.id not in web_load_balancer.elb.instances
  with_items: "{{ web_instances.tagged_instances }}"
```

We need to assign each of the instances we created in the task above to the load balancer. We loop over the instances variable again, as we did with the EIP task, and one by one attach the instances to the load balancer.

Running the above playbook will in turn run each of the tasks within it, gradually building up our resources.

If you change the count in the `ec2` task, and re-run the playbook, you'll notice that instances are created or removed depending on the count that currently exist.

## Provisioning our instances with Ansible

The best way to tie together this introduction is to provision our new EC2 instances with Ansible and set them up as web servers.

For this, we'll create another Ansible playbook with the specifics for the software configuration to apply to the instances, as well as using the Ansible dynamic inventory script so that we don't have to manually specify any of the instances we want to apply the configuration to. Ansible will be able to do this by us specifying tags that are assigned to instances.

In order for this to work, we need to download the dynamic inventory script to the same directoy as our playbook from here:

https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py

We then need to give the file execute permissions:

```sh
curl -o ec2.py \
  https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
chmod u+x ec2.py
```

The dynamic inventory script depends on a configuration file, so we download the default to the same directory also:

```sh
curl -o ec2.ini \
  https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini
```

Copy the below playbook file to `provision-infra.yml`:

```yml
---
- hosts: security_group_web_instances
  become: yes
  become_method: sudo
  remote_user: ubuntu

  tasks:
    - name: Install packages
      apt:
        name: "{{ item }}"
        update_cache: true
      with_items:
        - php5

    - name: Add a test PHP script
      copy:
        src: /var/www/index.php
        dest: /var/www/index.php
```

And then provision the instances by running the following command:

```sh
AWS_PROFILE=playground \
AWS_REGION=eu-west-1 \
ANSIBLE_HOST_KEY_CHECKING=false \
ANSIBLE_PRIVATE_KEY_FILE=web \
ansible-playbook -i ec2.py provision-infra.yml
```

Once completed, the instances should have PHP configured with a running test script. As we added a health check to our load balancer, once it detects the presence of the script, it will start serving traffic to that instance.

If you then access the public hostname of the load balancer, each time you refresh the page, you should see the hostname change.
