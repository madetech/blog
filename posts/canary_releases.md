# Canary Releases

At Made we employ Continuous Delivery practices to keep our software delivery fast and regular.

Continuous Delivery is an approach to software delivery which promotes small incremental releases rather than huge iterations. Every push to master which passes its test suite is considered to be production ready, and as a result our deployment pipeline is optimised to get it out to production websites as quickly as possible, without sacrificing security and safety. This benefits us as developers and our customers in the same ways. New features and bug fixes are deployed rapidly, and code is safer by virtue of having smaller changes. How much can you break in a day or two? We are all spared the anxiety of large, lengthy deploys where weeks of work can be released to production at once.

## What we're doing now

At the moment our process of Continuous Delivery is broken down into several steps.

- **Development** - We work on a new feature using a local copy of the app.
- **Build** - Pushing the new code to source control automatically triggers a build step, which runs our test suite, ensuring this code isn't going to break anything and we can safely release it.
- **Continuous** - The latest version of our app is hosted on a private server. This allows us to review it in an environment closer to the production one, and to have peer review from our colleagues. If we discover a bug here which our test suite didn't catch, we will go back to the first step and fix it.
- **Staging** - At this point we're happy with the state of our app. The feature is working as expected and any bugs we may have found are fixed. The latest version of the website is pushed to another private website where customers can review.
- **Production Test** - We currently employ "blue green" deploys, which means we can safely push changes to production without users seeing it. Instead a secondary production app is launched, connected to the same database as production. This is the final review step, if everything works here we're good to go live.
- **Production Flip** - We now point all users of the production website at the new production app, and switch off the old one. The new features are live!

This is a fairly complex setup, but it allows us to employ that rapid Continuous Delivery we love. Since we host most of our apps on Pivotal now, we wrote a gem called [cf-deploy][cf-deploy] to take care of most of these steps for us. Starting a new project is as simple installing cf-deploy, defining configuration for each stage, and hooking it into our deployment pipeline. In our case, Jenkins.

We have been using this for a while now, and we encourage you to try out the gem yourself!

## The benefits of Canary releases

Today we're excited by the concept of 'canary releases,' which promise to offer our customers and us more secure deployments, at a faster pace.

A 'canary release' is similar to a 'blue green' deployment in many key ways. New production candidate releases are pushed to a secondary production server, just as before. They share the same database, as before. But, significantly, a percentage of new users to the live website will instead be directed towards the canary release.

This allows us to test a production candidate with a subset of real users before committing to showing to all users. If our new changes have a bad effect, for example if they introduce a new error, we have the ability to pull the canary out and cancel the deploy. The live website is in the same state as it was before, and the error has only been exposed to a reduced number of users.

If the new app had instead been pushed directly to production, it would take longer to pull back and the damage could have potentially affected _all_ of our users.

The name, of course, comes from caged canaries which would be taken down into a mine by coal miners. If dangerous gases in the mine killed the canary, the miners would have sufficient warning to get out. In software delivery, canary production apps give us that same warning ahead of time.

Of course, just using a canary release doesn't remove any of our prior security nets. We still have peer review, customer review and production review stages before allowing new code into the wild. Crucially, canary releases give us an intermediate production release step which is much more powerful than 'blue green' deploys. Nobody can test your app better than real users.

## Our Canary strategy

Implementing canary releases means adjusting our deployment strategy. Our new process might look like this:

- **Development** - Same as before
- **Continuous** - Same as before
- **Staging** - Same as before
- **Canary Deploy** - A canary production release is spun up straight after staging, but not shown to any real users yet. This gives us an opportunity to check everything is okay first.
- **Canary Trial** - A percentage of traffic to our live website is directed to this canary instance, so we can test with a subset of users.

Following a trial, we have two options.
- **Canary Release** - Everything went well, new users on the canary website are not experiencing any new errors. The canary app scales up and replaces the old production app, all users are now on the latest version of production. This is analagous to the 'flip' step from before.
- **Canary Rollback** - Users on the canary website are experiencing errors, so we turn off the canary instance, and they are (invisibly) sent back to the old production site. All users are now on the existing production site and we can fix the bugs we caught before pushing again.

When connected to a Jenkins pipeline, the latter half of this deployment approach looks like this:

![Canaries!][jenkins-canary]

## Going forward

We are excited by the possibility of integrating canary releases into all of our clients' websites, and have built proof of concept deployment pipelines using this new approach. We are still experimenting with this, and haven't refined our approach to a production ready standard yet. That said, we have integrated the steps necessary for a fairly opinionated canary production release into an experimental 'canary-releases' branch of our [cf-deploy][cf-deploy-canary] gem. Give it a try and please let us know what you think!

[jenkins-canary]: https://www.dropbox.com/s/fe5yhi46znnvcmd/Screenshot%202015-10-02%2011.50.15.png?dl=1
[cf-deploy]: https://github.com/madetech/cf-deploy
[cf-deploy-canary]: https://github.com/madetech/cf-deploy/tree/canary-releases
