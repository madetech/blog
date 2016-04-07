# Build a CD Pipeline with Terraform and Ansible

Continuous Delivery pipelines are the norm at Made for the majority of our projects. It's common at the start of a project that we create a pipeline so that we're able to deploy the first versions of our applications all the way to a production, or production-like environment. 

In the past we've always done this setup manually each time, and as with all things you do manually, subtle differences creep in over time. We needed a way to automate this process so that firstly it would standardise our setups, and secondly, save us a lot of time. What used to take at least a couple of hours, can now be accomplished in a matter of minutes.

Using Terraform and Ansible, and with Makefile acting as a glue, we have a command that we can run, configurable with some variables, to get a Continuous Delivery Pipeline setup for a git repository by running `make jenkins`. Lets go behind the scenes and see what moving parts we have.

## Terraform

Terraform, by Hashicorp, the Vagrant people, allows you to write a manifest file containing a bunch of resources on AWS (or other providers). Such as EC2 Instances, Elastic IP's, security groups, key pairs etc. Defining these resources in code means it can be automated, and these manifest files also server as a form of documentation, illustrating what you have running.

At the very heart of a Terraform manifest file is the provider. This is where your infrastructure will be. AWS is the best supported, and you specify it with simply:

```
provider "aws" { }
```

You can specify a bunch of options in this block, such as the region you want to use, or the credentials profile, however, Terraform supports the use of environment variables for defining these, allowing us to have the most simple of declarations, and then let the user configure these by prefixing the command we run with environment variables such as `AWS_REGION=eu-west-1 make jenkins` as an example.

Coming back to our end goal of having a Continuous Delivery pipeline, we want to have an instance setup and configured with Jenkins. In our manifest file we specify:

```
resource "aws_instance" "jenkins_master" {
    ami = "ami-abc579d8"
    instance_type = "t2.micro"
    key_name = "${aws_key_pair.provisioner.key_name}"
    security_groups = ["${aws_security_group.ssh_and_http.name}"]

    tags {
        Name = "jenkins_master"
        role = "jenkins_master"
    }
}
```

This resource references a few others defined in the file, such as a key pair, and security groups, but the important thing to note here is the use of the tags block. We give the instance a Name, but also a custom tag called `role`.

## Ansible

Once Terraform has been run, we'll have our instance on AWS, but with nothing installed on it. Ansible is a provisioning tool that allows us to install and configure software on the instance.

Normally, you specify an inventory file for Ansible, which lists the hosts that are to be targetted. For me previously, this has always been a manual process, of grabbing the assigned IP address from AWS and then pasting it in the inventory file, and managing it completely by myself.

Ansible supports a Dynamic Inventory script. This is a small Python script that connects to AWS and pulls out the EC2 instances you have available. The important thing it does is group and assign these instances to Ansible groups based on the AWS tags you defined when creating them via Terraform.

In our Ansible playbook, we can specify the hosts to target, with the following:

```
- hosts: tag_role_jenkins_master
```

All roles and tasks under this will only be run on EC2 instances with the tag `role` and value of `jenkins_master`.

Now we're dynamically targetting the instances, we use Ansible to say what should be installed. We install a bunch of dependencies so that we can install Jenkins. We also use Ansible templates so that we can generate the XML files that Jenkins uses to create jobs for a git repository, and to configure the Build Pipeline plugin to create our Continuous Delivery pipeline.

## Makefile

Gluing all of this together is the Makefile. This allows us to define the dependencies of our tool by defining tasks and their dependencies. Breaking our Makefile down, we have a few tasks:

 * `build`: this runs terraform for us. In our terraform file we make a reference to a file that contains the SSH public key that we want added to the EC2 instance when it's created. This is then used by Ansible to SSH into the box to provision it. Therefore `build` has a dependency on the task `keys`.
 * `keys`: quite simply runs `ssh-keygen` for us to generate a brand new SSH key
 * `ansible`: we require the Dynamic Inventory script which requires a download and also to download some roles from Ansible Galaxy, so this task has dependencies on `ec2.py` and `ansible_roles`.
 * `ansible_roles`: this depends on each of the specific Ansible roles that we require to be downloaded
 * `provision`: this wraps up the `ansible-playbook` command that we need to run to have Ansible install our software. It prefixes the command with a bunch of configurable environment variables, as well as additional variables that will be used by the Ansible playbook when it's run. This includes the git repository URL of the project we want to use in our pipeline.
 * `jenkins`: this just ties our creation of infrastructure with the task `build` to our Ansible provisioning of `provision`. It defines those dependencies in that order so that Terraform is always run before Ansible.

## Creating your pipeline

```
make jenkins \
project_name='TestProject' \
jenkins_auth_user=jenkins \
jenkins_auth_password=testing \
repo='https://OAUTH_TOKEN_HERE:x-oauth-basic@github.com/YOUR_USERNAME/YOUR_REPO.git'
```

You can prefix this command with any additional AWS environment variables as mentioned above.

The Makefile itself takes four arguments:

 * `project_name`: This is used by the Jenkins pipeline view to give it a name visible from the Jenkins interface
 * `jenkins_auth_user`: When Ansible sets up Jenkins, it enables HTTP auth to protect it from the outside world, and this is the username that will be used
 * `jenkins_auth_password`: Along with the username, this is the password used for the HTTP auth security
 * `repo`: This is the project that will be used for the pipeline

## Notes and assumptions

 * Pipeline stages
 * Build and deploy commands
 * OAuth token for git

## Todo for tool

 * Support multiple projects/repos
 * DNS support to configure Jenkins at a domain
 * Custom build/deploy commands
 * Project build dependencies within Docker

## Open source

We've open sourced this project on [Github](https://github.com/madetech/terransible-jenkins). 

## Talk

I presented this tool at Infracoders a few weeks back, and if you're interested you can watch the video here and [view my slides here](https://speakerdeck.com/davidwinter/building-a-continuous-delivery-pipeline-in-5-minutes).
