# Creating a Better Rails Development Environment with Docker Compose

## Introduction
I've seen quite a few articles recently detailing the steps to creating a simple Ruby on Rails development environment without Vagrant. I've found a few issues with these that make the environment somewhat unfeasible for real use. Hopefully, by the end of this article you will have a Docker-based development environment that can actually be used for real development.

Today we'll be using [Docker](http://docker.io) and [docker-compose](https://docs.docker.com/compose/) to create a development environment around an existing Rails app. For this tutorial, we'll be linking the app's container to a separate db container to create a mini container cluster. This could then be extended to include memcached, redis, or other services so that your development environment can better replicate your production environment. Don't worry: it's not as hard as it sounds.

## Requirements

* A computer running a recent version of Mac OS X. I believe that the Docker toolbox works on Windows, but the steps may have to be adjusted if you are not running OS X.
* Git. This is needed to clone our Rails app repo. If you choose to use your own, you may have to modify the Dockerfile to `apt-get` more dependencies.
* Luckily, *no* previous experience with Docker is necessary.

## Setup

Download and install the [Docker Toolbox](https://www.docker.com/toolbox). Once this is done, you will have an app in Applications called 'Docker Quickstart Terminal'.

Open 'Docker Quickstart Terminal'. The first time this runs it should create a VM and set you up. If you prefer your own shell, you can use the following bash command:

```
eval $(docker-machine env default)
```

Clone our repository down and enter the folder:
```
git clone https://github.com/madetech/rails-docker-dev.git
cd rails-docker-dev
```

Use docker-compose to build the app

```
docker-compose build
```

This downloads the images you need from the Docker registry and creates the containers needed to run our app. Go and make a coffee. If you don't already have the images it will have to pull and build a LOT of stuff, which will take a quite a while.

Once that's done, create the database:

```
docker-compose run web rake db:create
```

Now it's time to launch the app. This command will launch the app. If you don't already have the db image it will pull that, but that is a small image and shouldn't take long.

```
docker-compose up
```

You can use the following command to get the ip of your docker host:

```
EXAMPLE:
$ echo $DOCKER_HOST
tcp://192.168.99.100:2376
```

Then you can visit that URL in the browser on port `3000` to see your app running!

```
EXAMPLE:
http://192.168.99.100:3000
```

For future convenience, you can then add that line to your `/etc/hosts` file to access your app more easily in future.

## Replacement Functions

As we're developing within Docker containers using docker-compose, we'll need to use a few different functions instead of our usual ones. I've included a few examples below.

| Original command | docker-compose command |
|--------------------|----------------------|
| `rails c`          | `docker-compose run web rails c` |
| `RAILS_ENV=test rake db:create` | `docker-compose run -e RAILS_ENV=test web rake db:create` |
| `rspec spec/path/to/spec.rb`    | `docker-compose run web rspec spec/path/to/spec.rb` |

## Conclusion

It's that easy! It's the quickest way I've found to set up a fully operational Rails app with database on a fresh laptop. No vagrant, no chef, no complicated build process, just pull and go. Next time we'll be diving into how this stuff works, and if there's any way to simplify this process even further. Stay tuned.
