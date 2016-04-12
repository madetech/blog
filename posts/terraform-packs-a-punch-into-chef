# Pack(er) all your things, grab your Chef, and lets go Terraform-ing

Here at Made we are always trying out new technologies that take the pain out of the common tasks we have to perform from project to project.

We’ve already discussed how we do this with our test automation, and our build pipeline. But until now the only manual task we’ve had to do repeatedly across all projects is provisioning infrastructure.

We have been using Chef to set up provision our infrastructure for a while now, but we have still had to log in to the AWS console and spin up the EC2 instances to run it against. Alongside all the other infrastructure requirements like RDS, S3, and load balancers.

For this we now can now use two Hashicorp tools - Packer and Terraform. These tools enable us to codify all of the configuration and commit it into source control. Having our infrasture as code, enables us to create identical server environments all the way up the deployment pipeline.

## Getting started?

Before we get started there are a couple of prerequisites we need in place.

- Login to AWS to create a new user in IAM for Terraform and Packer to use, be sure to download the credentials file, and store it in `~/.aws/credentials`. This is the standard location for AWS, and its also the default path both Packer, and Terraform. Its what I shall be using throughout to omit that configuration. Its worth mentioning that these credentials are what is used behind the scenes by the AWS libraries to create/destroy all the infrastructure.

- Generate a new SSH key pair. This SSH key will be used by Terraform, and added to the new EC2 instances. It will also allow us to SSH in and configure the newly created instances with Chef. When you generate the key pair you will need to specify a few additional attributes. `-f chef-provisioner` to specify a custom filename, `-P` to create a key pair without a passphrase, and `-m pem` to specify PEM format. The full command being `ssh-keygen -f chef-provisioner -e -m pem`

- Install Packer (https://www.packer.io/downloads.html), and Terraform (https://www.terraform.io/downloads.html).

## Building your AMI

Already having Chef set up makes building a machine image with Packer really simple. All we have to do is specify Chef Solo to be a provisioner, and configure the local relative paths.

```
{
  “provisioners”: [{
    "type": "chef-solo",
    “chef_environment”: “production”,
    “cookbook_paths”: “./cookbooks”,
    “data_bags_path”: “./data_bags”,
    “environments_path”: “./environments”,
    “roles_path”: “./roles”,
    "run_list": ["role[app]", "role[production]"],
    "staging_directory": "/home/ubuntu/cookbooks”,
    “skip_install”: false
  }]
}
```

Now we have the configuration for machine image, how can we make it available for use within Terraform? Packer provides a number of builders. In our use case we want to use the `amazon-eps` builder. This takes an existing Amazon AMI (ubuntu 14.04) and provisions on top of it.

```
"builders": [{
  "type": "amazon-ebs",
  "region": “eu-west-1",
  "source_ami": "ami-f95ef58a",
  "instance_type": “t2.nano",
  "ssh_username": "ubuntu",
  “ssh_private_key_file”: “path/to/generated/private_key",
  "ami_name": “made-project-ami {{timestamp}}"
}]
```

All that is left to do is run `packer build path/to/packer.json`. Once packer has finished it will spit out the generated AMI reference.

Lets Terraform this...

```
provider "aws" {
  region = “eu-west-1"
}

resource "aws_key_pair” "chef" {
  key_name = “chef-provisioner"
  public_key = “your public key file"
}
```

You can further dry up the `aws_key_pair` definition using the `file` function which is one of the interpolation functions (https://www.terraform.io/docs/configuration/interpolation.html) built into terraform.

```
variable “azs" {
  default = {
      zone0 = “eu-west-1a"
      zone1 = “eu-west-1b"
  }
}

resource "aws_security_group” "app” {
  name = "app_sg"

  # here be security rules
}

resource "aws_instance” “app" {
  ami = “ami-m4d3am1” # Not a real AMI
  availability_zone = "${lookup(var.azs, concat("zone", count.index))}"
  count = 2
  instance_type = “t2.nano” # Can be any Amazon instance size
  key_name = "${aws_key_pair.chef.key_name}"
  security_groups = ["${aws_security_group.app.name}"]
  tags {
    Name = “${concat(“web_app_", count.index)}"
  }
}

resource “aws_eip" "app_ip" {
  count = 2
  instance = "${element(aws_instance.app.*.id, count.index)}"
  vpc = true
}
```

You’ll notice we have specified the availability zones for the instances above, this is to guarantee maximum availability of our app, by ensuring are spinning up instances in multiple availability zones within our AWS region.

In order to open up our instances to the world, alongside the aws_instance resource declaration, there is an elastic IP being defined, and to secure the whole set up there is a security group defined.

Taking this further

A great iteration on this would be go get Packer to build a AMI of each successful deploy to production using the base box we built earlier on. To do this all we’d need to do would be to add an additional provisioner to checkout the latest stable production build, execute and execute the necessary commands, e.g. `bundle install`. So what does benefit would this have? Well this mean our application could scale up very quickly and we would always have a current production (or staging) AMI ready to go.

Continuing with Packer improvements another direction to take this would be add the Atlas (another Hashicorp tool) (post processor)[https://www.packer.io/docs/post-processors/atlas.html] to the Packer json to register for Altas Enterprise and leverage its - Atlas’s - artefact directory to always serve the “latest” production artefact to Terraform (https://www.terraform.io/docs/providers/atlas/r/artifact.html). This would also hopefully take care of housekeeping all the older production machine images.
