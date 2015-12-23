#Continuous Delivery Tools

Finding the right platform to form the basis of your Continuous Delivery is key, And you really need a solution that is going to fit into your existing way of working with minimal effort.

In this article, we'll discuss the key features which are fundamental to running a successful Continuous Delivery pipeline, and some of the - open source - self-hosted and [Software as a Service](https://en.wikipedia.org/wiki/Software_as_a_service) (SaaS) solutions on the market.

## Selecting your solution

When choosing your solution, be it SaaS or self-hosted, you need to have confidence that it will offer you and your team a pain free Continuous Delivery work flow.

Factors that can influence this decision will range from the amount of work needed for initial setup, to the time it will take to undertake any ongoing maintenance, and finally how easily it integrates with your PaaS or server infrastructure.

Whilst it's great to shop about you really want to get it right first time, as you don't want to invest project time on an "Ok" solution that you will have to migrate away from 6 months down the line.

##Essential Features
Whilst every SaaS or self-hosted solution on the market boast a myriad of different feature sets, there are a handful of core features that are essential to operating a successful pipeline.

###Integration with version control
Version control integration is the most crucial feature your chosen solution should possess. When I say integration, I mean it should poll your repository, or use web hooks to detect changes, which should then initiate a new build and subsequently trigger the rest of your CD pipeline process.

###Custom script execution
Custom script execution within a pipeline step is a key feature especially if you deliver a diverse number of projects.

Thanks to [buildpacks](http://docs.cloudfoundry.org/buildpacks/) many common deployments are very simple, but often the need arises to run custom deploy scripts. In these instances the ability to use tools like [Capistrano](http://capistranorb.com/documentation/overview/what-is-capistrano/) to execute deployment tasks is vital. While it is written in ruby it can be used to deploy almost any project, thanks to the open source community behind it.

###A Pipeline
A pipeline view is a visual representation of all you deployment steps. These steps should all be linear. A single step, e.g. unit testing, could fan out to run multiple tests in parallel. Then any dependent step should be executed automatically once the previous steps have passed. The final step in the process should be a manual one, in order for one of the team to make certain that the build is in a good state before releasing to any publicly facing environment.

###Notifications
As a software engineer, switching contexts can be really distracting so your continuous delivery solution should offer an alerting system to inform your team to any successful or failed deploys without them needing to check a web interface.

In a basic form this can manifest itself as a simple email, however many continuous delivery platforms will also integrate with the popular team chat programs, like HipChat and Slack.

##Self Hosted vs SaaS
The argument for self-hosted or SaaS solutions will not be resolved in this article, as both have their flaws, and their advantages.

A self-hosted solution for example will require a lot more initial set up than a SaaS solution, as most of these are one click installs, and simple to configure using a YAML file (or similar).

However the up front investment in infrastructure, and other set up required with a self-hosted solution will be netted out over a number of projects, and will allow you flexibility in the long term as you are free to add features provided from community plugins and extensions. This is flexibility you just don't get with a SaaS solution, where you are tied to their feature set and development cycle of adding new features.

##Options
Having discussed the recommended features (and pitfalls) of both options, below is a selection of solutions that provide said features, which the market currently offers:

###Self Hosted

####Jenkins CI (https://jenkins-ci.org/)
Whilst technically a [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration) platform, with the addition of the [build pipeline plugin](https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin) it is easily configured to be a complete Continuous Integration and Continuous Delivery solution.

####Go (https://www.go.cd/)
Go is a Continuous Delivery platform written and maintained by the folks at ThoughtWorks, who literally wrote the book on Continuous Delivery, so as you can imagine Go is based on a lot of the principles outlined in it. Like Jenkins (with the build pipeline plugins) it will perform both Continuous Integration and Continuous Delivery.

####Spinnaker (https://github.com/spinnaker/spinnaker)
The newest option in the list - Spinnaker - differs from the previous two as it is only a Continuous Delivery platform. Spinnaker will take a deployable asset (e.g. a Docker image) and deploy it out though the pipeline steps, but only once it has received trigger from a separate CI platform like Jenkins.

###SaaS

####Cloudbees (https://www.cloudbees.com)
Cloudbees is Jenkins in the cloud. Cloudbees uses a [Workflow plugin](http://documentation.cloudbees.com/docs/cje-user-guide/workflow.html) - which you could implement on your self-hosted Jenkins instance - to add Continuous Delivery functionality. So if you like your self-hosted Jenkins but no longer want to maintain the infrastructure, then this could be an option for you.

####Snap CI (https://snap-ci.com/)
Snap like many SaaS offerings is tied to GitHub (at time of writing). Snap enables you to build both simple linear pipelines, and advanced branched pipelines from either a single, or multiple repositories.

####Harrow IO (https://www.harrow.io/)
Harrow IO a SaaS solution from the folks that maintain Capistrano. Whilst you can use any script to run your integration, and delivery steps Harrow provides simple integration if you are already using Capistrano scripts to execute deployments.

##Summary
