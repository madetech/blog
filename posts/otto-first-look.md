# Otto: first look

Otto is marketed as the successor to Vagrant, the development tool that has been used by developers across the globe for the past five years. When it was first released it took the industry by storm because it allowed self-contained virtualised development environments that didn't require you to worry about installing tools on your computer's actual operating system. It also allowed you to match your production environments more closely by being able to mirror the operating system and by provisioning the Vagrant machines using the same tools you'd use for production servers (Ansible, Chef, Puppet etc.)

Five years is a long time in terms of technology. Docker has come along in this time and allowed for a similar concept of self-contained environments for your apps. With Docker, you can use the same container/image to deploy straight out to production, and [docker compose](https://docs.docker.com/compose/) is beginning to make adoption of this much simpler.

PaaS providers have also grown in this time. Heroku is still as popular as ever, and with tools such as [Wercker](http://wercker.com/) gaining traction, the line between development and production environments is blurring even more so. If you haven't already, go and read my colleague, Chris' article on [IaaS vs. PaaS](https://www.madetech.com/blog/iaas-vs-paas-what-weve-learned)

Otto, along with claiming to replace Vagrant, also intends to make the jump across the line between development and production a much easier one to tackle. Using a mixture of [Hashicorp tooling](https://ottoproject.io/intro/index.html), you can develop an application, create infrastructure and deploy your application all with one tool. It looks very promising, and as only a 0.1 version was released the other day, we can expect lots to come and changes to be made as the developers receive feedback.

In this first look article, I'm going to focus on the development side of Otto and how it currently fares as a Vagrant replacement.

## Development

Under the hood Otto is still using Vagrant. When you setup Otto using `otto compile` it will take a stab at detecting the type of application you're developing; Ruby, PHP, Node for example. I was playing with Otto using an existing Ruby application with the intention of being able to convert it to an Otto project.

Otto will create a bunch of setup files within a `.otto` directory in your project. For the development side of things, this means it creates a `Vagrantfile` that uses [Shell provisioning](https://github.com/hashicorp/otto/blob/master/builtin/app/ruby/data/common/dev/Vagrantfile.tpl) to install the tooling for the project, such as [Ruby and bundler](https://ottoproject.io/docs/apps/ruby/dev.html).

If your project requires any packages or configuration other than those specified in the predefined application type, there is currently no easy way of changing this. The two options you have is to specify a [custom application type](https://ottoproject.io/docs/apps/custom/index.html) that uses a `Vagrantfile` with your specific needs, or, \*gulp\*, `ssh` into the machine and install manually with `apt`.

Specifying a custom `Vagrantfile` would also then give you the option to specify any other customisations, such as memory and CPU values, which can't currently be done via any of the Otto customisations. This was a frustration I run into when I was trying to seed a database with data. Currently, if needing to specify a `Vagrantfile` for use with Otto, I don't see how it can currently replace Vagrant itself.

So if your project uses MySQL rather than Postgres, then you're currently in for a rough ride and it might be best to hold out for the project to mature. Hopefully it's not a big deal, as it should be just a case of adding `libmysqlclient-dev` to the otto setup so that the `mysql2` gem can communicate with a MySQL server.

Assuming that happens, the next step would be to define MySQL as a dependency of the app. The otto documentation has an example of using Mongo, so adapting that for MySQL was quite simple by creating the following Appfile inside a new directory I created `private/otto/mysql/Appfile`:

```
application {
    name = "mysql"
    type = "docker-external"
}

customization "mysql" {
    image = "mysql"
    run_args = "-e MYSQL_ROOT_PASSWORD=my-secret-pw -e MYSQL_DATABASE=localdev -p 3306:3306"
}
```

This uses a docker MySQL image that otto will configure with some environment variables to setup the machine.

Then back in our main `Appfile` we reference the dependency like so:

```
application {
  name = "testproject"
  type = "ruby"

  dependency { source = "mysql" }
}
```

**There appears to currently be a bug where the `run_args` aren't be compiled into the application `Vagrantfile` - based on the Mongo example. Awaiting comment/clarification.**

You can then start the development environment with `otto dev` and updating your `database.yml` file to reference the MySQL host with the hostname of `mysql.service.consul`.

This dependency configuration all seems very similar to the way `docker-compose` and `wercker` are setup. However, otto seems currently less flexible, though it is early days.

Making changes in otto currently [require a destroy and rebuild](https://ottoproject.io/intro/getting-started/customization.html
) of the entire machine. So you don't currently get the speed of a `vagrant provision` as you might be familiar with in your current setups.

Once you have an otto environment up and running, you are ready to `otto dev ssh` and run a bundle install and get your server running. Run `otto dev address` to get the IP address assigned to the machine and then you can visit it directly in your browser. Continue developing away at this point.

***

Otto is currently a 0.1 release. It's nowhere near ready to replace Vagrant in most developers day-to-day work if you need to deviate from the supported [App types](https://ottoproject.io/docs/apps/index.html), but has given us a good idea of what is in store. When plugins are introduced in the next release, a lot of the quirks and hurdles I encountered I'm sure will be ironed out. We'll be keeping a close eye on it as it develops.
