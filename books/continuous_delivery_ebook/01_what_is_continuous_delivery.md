# What is Continuous Delivery?

In today's world of instant communication, businesses need to be able to move quickly to meet the ever changing needs of their customers, especially so when it comes to building, maintaining and evolving the online platforms of those businesses.

Past development practices didn't always lend themselves to this fact, with releases taking place weeks or even months apart, and huge changesets being the norm.

At its inception, the goal of Continuous Delivery was to find a way to optimise those practices to the point where small, iterative releases could happen, and that those releases are be safely deployable to a production environment at any time, and _are_ deployed as often as several times a day.

For businesses, this is incredibly valuable, in that they are then able to get features to, and feedback from, their customers at a much faster rate. For developers, they can be confident that what used to be a very painful process is now simple, mundane even, and that the code they release is stable.

## Where did Continuous Delivery come from?

In a nutshell, Continuous Delivery was borne, many eons ago (i.e. within the last twenty years), out of the frustration of developers stuck in what was known as 'Integration Hell', the point at which the code you've been working on for the last few weeks meets the code that the rest of your team has been working on in that period, and the point at which you realise those two code bases are incompatible in subtle and sometimes devastating ways.

It used to be that a project would be worked on by a team of developers who each went away work on their own area of code for periods of weeks or even months at a time, after which all of the work would be brought together, and everyone would knowingly walk into Integration Hell. Developers are problem solvers by nature and, as a huge pain point, this was a problem that very much needed to be solved.

### Automation For The People

One such solution was [Steve McConnell's 'Daily Build and Smoke Test'](http://www.stevemcconnell.com/ieeesoftware/bp04.htm), from 1996. His idea was for all code to be tested at the end of every day and run as a 'smoke test', an automated process that immediately 'broke the build' should it find any fundamental problems.

His reasoning was that if anything _did_ break, chances were that it would be much simpler to fix something that had cropped up in the last 24 hours than it would be to fix something that had occurred at some point within the last month.

The idea struck a chord, and later, over at [Thoughtworks](https://www.thoughtworks.com/), Matt Foemmel, along with Martin Fowler, took a similar concept introduced by the [Extreme Programming](https://en.wikipedia.org/wiki/Extreme_programming) methodology and developed it into something much bigger. This concept was called [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration) (not to be confused with Continuous _Delivery_).

The pair wrote about their experiences in [this popular article](http://www.martinfowler.com/articles/originalContinuousIntegration.html), the broad strokes being that developers should be contributing code to a single repository under source control, which then, automatically, runs a series of tests, followed by a build on success.

While the build and testing steps are automated, there is still (and most likely always will be) a necessarily manual step to all of this, in that individual developers are themselves responsible for reintegrating several times a day.

Integration problems will still occasionally arise, it just means that when they do occur, they occur early, and are usually small enough to prevent another trip into Integration Hell, making the entire process demonstrably less painful for everyone.

As an added bonus, the fact that all of the code is committed to a single repository means that new developers can join the project without needing to spend days setting up a development environment, again increasing the speed at which a project can move.

### So, what is Continuous Delivery?

Where Continuous _Integration_ is about making it easier for multiple developers to work on the same project together, Continuous Delivery is about how we make it easy to get that work quickly and safely to production, and out into the wild, actually delivering value to Product Owners and their users.

This transition from development to production is facilitated by what's known as a build pipeline, which houses a number of different 'environments'. The pipeline handles the process of advancing our code through each of these environments, whereby upon a successful build in a given environment (which includes our automated tests), we are then able to trigger a build in the next environment, either automatically or manually.

Each environment serves a different purpose, and different development teams will create pipelines with any number of environments to meet their needs. What's important is that the pipeline is set up in such a way that developers can road test their code in a production-like environment, with production-like data, and that new features can be previewed and tested by the Product Owner. The ultimate destination for our code is, of course, the production environment.

What Continuous Delivery is, then, is the ability to push that code through the build pipeline all the way to production, with confidence, at a moment's notice. While the Product Owner may not want those new features to go live just yet, by getting the code successfully all the way through to the staging environment and having both you and the Product Owner review it, you can be sure that when you _are_ given the go ahead, the push to production will be a painless one.
