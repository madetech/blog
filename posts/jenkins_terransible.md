# Build a CD Pipeline with Terraform and Ansible

At Made, the majority of our projects use Continuous Delivery pipelines to provide a clear path to deploying to production. It's common for these to be setup on the first day of a project kick-off.

In the past we've always setup these manually, and as with all things you do manually, subtle differences creep in over time. We needed a way to automate this process so that firstly it would standardise our setups, and secondly, save us a lot of time. What used to take at least a couple of hours, can now be accomplished in a matter of minutes.

Using Terraform and Ansible, and with a Makefile acting as glue, we have a command that we can run, configurable with some variables, to get a Continuous Delivery Pipeline setup for a git repository by running `make jenkins`. The basic flow of the tool is:

 1. Create an SSH keypair used on AWS EC2 instance
 2. Using Terraform, create AWS resources
 3. Have Ansible connect to EC2 instances and install and configure Jenkins
 4. Configure a Jenkins build pipeline using common pipeline steps, as described below, for a specified git project repository.

We use a standard pipeline structure which consists of a few steps:

 1. **Build** to runs tests and code checks
 2. **Continuous** environment deploy
 3. **Staging** environment deploy
 4. **Production** environment deploy

These steps are of one of two types; a _build_ or _deploy_ step. 

The tool we've made expects projects to have two files:

 * `bin/build` - used for the _build_ step
 * `bin/deploy <env>` - used to for the _deploy_ steps, where `<env>` is one of `continuous`, `staging` or `production`.

By using this interface for projects, Jenkins needs to know nothing about how to build or deploy. It just triggers these scripts at each step.

That's a brief overview of the tool and what it achieves. Now lets break it down into more detail for each of the tools we use.

## SSH Key

Setting up an SSH key for the instances that Terraform will create is an essential first step. Using `ssh-keygen` we generate a new key and store it on the local filesystem. Our Terraform configuration will use this to setup a keypair on AWS, which will then be used on the new instance it'll create. This adds the public key to the `authorized_keys` file on the new EC2 instance, allowing Ansible to connect further on to install and configure Jenkins.

When you normally run `ssh-keygen` it gives you an interactive prompt to complete the setup. We want to automate that, so we use two different flags. Using `-f` allows us to specify the location where the key will be saved. And `-P` allows us to specify an empty passphrase.

## Terraform

[Terraform](https://www.terraform.io/), by Hashicorp, the Vagrant people, allows you to write a configuration file containing a bunch of resources which represent infrastructure. AWS is the best supported provider with Terraform, so we're using that for this. Terraform resources can be things such as EC2 Instances, Elastic IP's, security groups or key pairs. Defining these resources in code means it can be automated, and these configuration files also serve as a form of documentation.

At the very heart of a Terraform configuration file is the provider. This is where your infrastructure will be. You specify it with the following:

```
provider "aws" { }
```

You can specify a bunch of options in this block, such as the region you want to use, and API credentials, however, Terraform supports the use of [environment variables](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-environment) for defining these, allowing us to have the most simple of declarations, and then let the user configure these by prefixing the command we run with environment variables such as `AWS_REGION=eu-west-1 make jenkins`.

Our configuration file sets up a single EC2 instance to run Jenkins:

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

```
tags {
    Name = "jenkins_master"
    role = "jenkins_master"
}
```

The keypair that Terraform will use is defined in the following resource:

```
resource "aws_key_pair" "provisioner" {
  key_name = "terransible_provisioner"
  public_key = "${file("keys/terransible_provisioner.pub")}"
}
```

You'll notice that `${file("keys/terransible_provisioner.pub")}` is used to get the contents of the public key file that we generated with `ssh-keygen`.

## Ansible

Once Terraform has run, we'll have an instance on AWS, but with nothing installed or configured on it, besides the SSH key. 

[Ansible](http://docs.ansible.com/ansible/) is a provisioning tool, similar to Puppet or Chef, that allows us to install and configure software on the instance.

Ansible is configured to use the same SSH key that we created in the first step, so that it's able to connect to the instance. But how does Ansible know which instances to connect to?

Normally, you specify an inventory file for Ansible, which lists the hosts that are to be targetted. This is normally a manual process, of grabbing the assigned IP address of an EC2 instance from AWS and then pasting it in the inventory file, and managing it completely by hand.

Ansible supports a [Dynamic Inventory script](http://docs.ansible.com/ansible/intro_dynamic_inventory.html#example-aws-ec2-external-inventory-script). This is a small Python script that connects to AWS and pulls out the EC2 instances you have available. The important thing it does is group and assign these instances to Ansible groups based on the AWS tags you defined when creating them via Terraform.

In our Ansible playbook, we can specify the hosts to target, with the following:

```
- hosts: tag_role_jenkins_master
```

All roles and tasks under this will only be run on EC2 instances with the tag `role` and value of `jenkins_master`.

Now we're dynamically targetting the instances, we use Ansible to say what should be installed. We install a bunch of dependencies so that we can install Jenkins. 

We use Ansible templates so that we can generate the XML files that Jenkins uses to create jobs for the git repository of our project, and to configure the Build Pipeline plugin to create our Continuous Delivery pipeline based on the steps mentioned earlier.

## Makefile

Gluing all of this together is the Makefile. This allows us to define the dependencies of our tool by defining tasks and their dependencies. Breaking our Makefile down, we have a few tasks:

 * `keys`: uses `ssh-keygen` to generate an SSH key
 * `build`: this runs terraform for us. In our terraform file we make a reference to a file that contains the SSH public key that we want added to the EC2 instance when it's created. This is then used by Ansible to SSH into the box to provision it. Therefore `build` has a dependency on the task `keys`.
 * `ansible`: downloads the dynamic inventory script and also some Ansible roles from [Ansible Galaxy](https://galaxy.ansible.com/)
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

Currently, to make setup easier, we use HTTPS to clone the git repository, using an OAuth token, which means we don't need to worry about SSH key setup to connect to Github.

After the `make jenkins` command has finished, in the Ansible output, there'll be an IP address. You can then visit that in a browser, where you'll be prompted with an authentication prompt, where you can supply the HTTP auth credentials to login to your pipeline.

## Taking it further

We're still developing this tool, and in it's current form, which was a proof-of-concept, we have plans to build on top of it support for the following:

 * Support multiple projects/repos. Currently this tool only accepts one git repository. We'd like to be able to support multiple, in turn creating multiple pipelines on a single Jenkins.
 * Ability to add Jenkins slaves rather than everything run on one instance.
 * DNS support to configure Jenkins to be served at a domain.
 * Project build dependencies. Currently, we only support Ruby based apps with common Ruby dependencies. We'd like to isolate these within Docker, or something similar so that any type of project can be built/deployed.

Over the coming months, we hope to introduce these and other features. We've open sourced all of the code on our [Github](https://github.com/madetech/terransible-jenkins) and welcome feedback, feature requests and PR's!

## Infracoders talk

I presented this tool at Infracoders on the 16th of March and you can find the [video here](https://skillsmatter.com/skillscasts/7630-terraform-to-build-infrastructure-in-aws) and view my slides on [Speakerdeck](https://speakerdeck.com/davidwinter/building-a-continuous-delivery-pipeline-in-5-minutes).
