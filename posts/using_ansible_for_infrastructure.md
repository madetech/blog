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


 * Ansible playbook using the localhost host
 * Managing AWS credentials
 * Building resources
 * Lack of state file - querying resources direct from AWS
 * Querying resources to be more dynamic; set_fact etc
 * Tying into provisioning/configuration of servers
	 * Dynamic inventory script
