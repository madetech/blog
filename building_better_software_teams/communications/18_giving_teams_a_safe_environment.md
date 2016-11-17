# Giving teams an environment where everyone can deploy safely any time

Developers should be allowed to deploy at any time. Many find this a scary prospect since it makes traditional release management and QA very hard. We have found that empowering developers to own the responsibility of deployment allows you to ship software much faster whilst maintaining or even improving the safety of releasing changes when compared to more traditional processes.

As part of our mission to improve software delivery in every organisation we seek to bring our customers on a journey from deploying once a quarter to a few times a day.

## What do we mean by deploying safely at any time?

Anyone who introduces a new feature, makes an improvement or fixes a bug should be allowed to push that change into production and should take responsibility for that change. The engineer will not only make a change to the code but deploy it, ensure that it functions as expected in production and even be in touch with the stakeholders of the feature whether they be customers or colleagues to announce the changes. Should anything go wrong, they are responsible for fixing it.

There are many safe guards that accompany a continuous deployment practice. We for example have a production-like environment that we test against before putting changes live. We also have automated testing and code reviews where other engineers are asked to review work before it's allow to be released.

## Why should everyone deploy their own changes?

Before going into the details of explaining how to create a safe environment it's probably best we answer the "why" first.

The biggest benefit when empowering teams to deploy more often is that change becomes less risky. By making more frequent changes they will naturally be smaller. If our deployments are smaller they will be easier to test and easier to fix in the case of any issues. Deployments should become mundane.

Over time your team will become better at testing their own changes and fixing issues when they arise. When a developer releases a change they will learn to become responsible for testing and monitoring it. This creates a proactive culture where developers can quickly react to problems often allowing them to spot defects before many users encounter them.

Releasing more often also means changes get into the hands of your users faster. Removing overheads such as QA processes means that we can make changes quickly, reacting to market changes and the metrics we collect.

> empowered developers are happier developers

Not only do the business and customers benefit from more frequent releases but we've found empowered developers are happier developers. By being responsible for a change, from start to finish, developers will feel a sense of pride and ownership over their work. We've found more traditional release strategies lead to developers passing responsibility onto QA or the deployment teams, simply throwing their work over the fence. When developers own their changes, they will put care into their work.

One common argument that may come up is that developers will be swapping depth of knowlege in a particular field for breadth which spans many fields. While this is a reasonable concern we have found that this is not as drastic as it may seem and almost always engineers prefer the responsibility of owning the whole problem.

## How do you provide a safe deployment environment?

From our experiences we have found the following 6 steps to greatly improve the way in which software is deployed. These can be expanded on but having these in place will greatly benefit your releases.

 - Create a safe environment where it is ok to fail
 - Make deployments easier by automating them
 - Ensure the deployment pipeline is fast
 - Deploy to a production-like environment for testing before going live
 - Get used to deploying small changes
 - Tell everyone about your deployments when they happen
 - Set up monitoring so you know when you deploy a breaking change
 - Use blue green deployments so rolling back is easy

We'll now briefly go into each one of these subjects although each could, and in some cases do, have entire blog posts about them.

### Encourage a culture where it is ok to fail

In order to benefit from deploying faster, you first need a culture where failure is ok. It is rare in software engineering that changes are perfect first time round. Optimising for fixing failures quickly provides more value than getting things right the first time round. This is sometimes called optimising for MTTR (Mean Time To Repair) rather than MTBF (Mean Time Between Failures).

Failure can often lead to blame. Instead of making failure a negative situation everyone in your team should understand that failure happens and is in fact a great opportunity to learn from and develop. When failure happens, the team should stand together, jump on the problem as a team and then discuss what happened afterwards with the aim of improving things for the future.

When you have a friendly environment for people to work in, they will produce better work. Don't punish failure, reward recovery.

### Make deployments easier by automating them

Humans aren't great at repeating processes, and let's face it, repeating yourself can be boring too. A typical deployment will include building, testing and releasing the software to the public. Each of these steps are themselves made up of a series of smaller steps.

Use scripts for each step in your pipeline so each step can be executed with one command. You can use services like Travis CI, Circle CI and Codeship, or self-hosted solutions like Jenkins to run scripts automatically for you. For example when a new change has been peer reviewed and accepted by merging the change into the main codebase, code hosting platforms like GitHub can automatically trigger your build and testing scripts for you.

Deployment scripts can be triggered manually or automatically when the previous steps are completed. Even if an engineer has to click a button to put a change live, that's a lot less error prone than running scripts, or a sequence of commands manually.

### Ensure the deployment pipeline is fast

When a problem occurs in production, you'll want to fix it as quick as you can. Once diagnosis of the problem has occurred, and a fix applied locally, you'll want to ship that change out fast. In order to do this your pipeline needs to be quick too. Even larger projects should only be taking 10-20 minutes to go through the pipeline with the ideal speed being much lower than that.

Being able to react fast can often mean rather than needing to roll back, you can in fact roll forward. In reality this means rather than removing a new feature when you find an issue you can instead fix it quickly. Of course, if it's a more serious problem, rolling back or disabling the feature would most likely be the correct course of action.

### Deploy to a production-like environment for testing before going live

Before putting a change live that has only been run on an developer or two's laptop, you'll want an environment that you can test it on that mimics production. Often local development configuration will use different settings and modes, particular when it comes to what type of databases it uses and debugging settings. A change in these conditions like when an application moves from development to production can be a source of errors. You'll want a production-like setup in order to discover these errors before things go live.

In order to facilitate a production-like environment ideally everything from server setup, database configuration, data stored in the database should be nearly identical to production. One consideration with data is that you may want to copy data from production into your production-like environment but you'll want to replace customer emails with example ones otherwise you may end up sending emails to customers from your production-like environment.

### Get used to deploying small changes

When deploys are kept small, to something like 100-200 lines of code or smaller, risk is limited. It's fairly obvious that when your changes only impact a smaller surface area of a system, when something goes wrong, there will be a smaller area to search within to find the problem.

Smaller changes will also mean that peer reviewing and testing are a quicker process. Again a smaller surface area is easier to look over, easier to test the various pathways through it.

To reduce risk, instead of deploying whole features, deploy 10s of times before the feature is complete. You do not need to make the feature publicly accessible until the last release but by dark launching it into production you will be uncovering a lot of problems early, avoiding the big bang release and the problems that come with it.

### Tell everyone about your deploys when they happen

If you have automated your deploys, you'll also be able to automate the broadcasting of this deploy. It is important to let everyone know about change when it happens so everyone can have a look at the new functionality, be alert and ready for when any issues occur, and also to celebrate yet another release.

You could consider automatically emailing the team and wider business when changes go live. If you use chat applications like Slack you could set up alerts within appropriate channels. You could even start emailing your customers automatically if you're brave.

### Set up monitoring so you know when you deploy a breaking change

You need good monitoring in your application so that when an error occurs, or page load of a web application slows down, you are alerted to the problem. After any deploy to production, the developer who pushed it up should keep an eye on the monitoring to see if any defects had been introduced but should also be notified automatically of any such issues.

Since the nature of change does carry some risk the goal is to spot potential defects before the issue affects a greater number of people.

Tools such as NewRelic allow you to set up alerts when certain performance thresholds are exceeded along with notifying of errors that happen to applications.

### Use blue green deployments so rolling back is easy

If you deploy frequently and monitor the system after each deploy, you should have a pretty clear picture on which deploy had adverse effects on the
system. If you have a fast pipeline, you'll likely be able to roll forward if the issue isn't too great. But what if you do need to rollback?

Using blue green deployments is a safe way to deploy a new production. Essentially when you have a new release ready you deploy it to a new server rather than immediately replacing the old production server. You can then visit this version of the application, make sure it's okay, then point the domain name of production at the new server thereby switching web traffic over to the new version.

Blue green deployments have the benefit that if something goes wrong, you can point the domain back at the old version again in order to rollback. Of course it also gives you another opportunity to test your changes before showing them to the world.

## Trust your teams

It all comes down to trust. Developers should be allowed to deploy at any time in most cases. We should learn to recover from failure fast, and learn all the lessons failure can teach us.

Let me know what you think on Twitter @LukeMorton :)
