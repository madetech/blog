# Keeping a clear path to production

In order to enjoy the benefits of Continuous Delivery it is imperative to be
able to deploy all the way to production at any time. Any reason as to why you
cannot deploy to production is a blocker. Keeping the pathway clear is also
the hardest part of implementing and maintaining a continuous delivery of
software.

## Broken builds

The first step of a Continuous Delivery pipeline is the build step. A typical
build step will run your tests, check the style of your code, point out overly
complex methods and more. This means your build step has a lot of ways to fail.
This is a Good Thing because it catches issues early but also means it's a
prime candidate for blocker status.

The solution to broken builds is obvious, you fix them and you fix them fast.
We have a rule at Made Tech that you must own your build failure. As soon as
the build breaks you tell your colleagues in Slack that you are looking into
it. You drop whatever you are doing and try to fix it immediately. If you
cannot fix the problem quickly you back your changes out with a `git revert`
or something similar.

Preventative measures can be taken to reduce the likelihood of broken builds.
Your developers can run the build script locally. We usually have a rake task
that our build server runs so this can easily be run locally too.

Parity between environments is also important. Running your tests locally and
seeing them pass to then see them fail when they run on the build server is
never fun. We have found bugs can arise from using different databases in
development from test, for example running SQLite in test but MySQL everywhere
else. Where possible use the same database management system everywhere. Same
goes for asset storage, if you use Amazon S3 for file storage in production
you better use it in development and test too.

### On flickering builds

In the past we have suffered from flickering tests. These are tests that
sometimes pass and sometimes fail. Often the cause will be a test that sets
up state and does not clear it down afterwards therefore affecting the result
of a subsequent test run. Another cause we have found to be tests that run
in headless browsers like Selenium, PhantomJS and the like. Sometimes
expectations on page content will fail because an asynchronous request has
not completed yet and therefore hasn't changed the page content as expected yet.

The nature of flickering tests is corrosive to Continuous Delivery discipline.
You will often find engineers just rerun tests several times in the hope they
will pass. This obviously affects the clear path to production. Also if your
build could fail at any time, and if your build time is in the tens of minutes
(another problem for another time) a flickering test can really slow you down.

The cure to flickering tests is to either resolve their flickering nature as
soon as you notice them or delete them. Removing the test is better than 
having it flicker due to its ability to disparage your engineers.

## Work In Progress

We encourage our engineers to push early and often. This means you commit small
chunks of work and push them to your project's master branch several times an
hour. We encourage this to avoid merge hell as discussed in the previous chapter
and also to encourage limited work in progress.

The problem with your engineers pushing code is that the tests may pass but
the feature is not necessarily complete enough to be released to users.
Incomplete work in your master branch that would affect a user is a blocker.

We practice dark launching of code regularly to circumvent this. Dark launching
simply means the code is able to be deployed out to production but it is never
accessed by users. The simplest way to dark launch a new feature is to release
it under a new URL and not link to the URL from anywhere. This might seem crude
but it works very well for us.

Feature toggles are a more advanced way of dark launching. Simply wrap up your
feature in a toggle and ensure it is disabled in production. We tend to use
feature toggles if a feature is a change to an existing feature or is provided
by a URL already accessible to users.

## Unreviewed work

We have found that sometimes features can sit complete on staging, undeployable
to production since the feature requires verification from a Customer, Product
Owner or a colleague that has not gotten round to it yet. The external
dependency on a Customer can really block your pipeline.

If you have limited reviews by Customers before deployment to production you are
in luck. In these situations we encourage engineers to not move onto another
task until the one they have just completed is reviewed. In fact we consider it
incomplete until it's reviewed and deployed to production. This often forces
the engineer to get up and get a colleague to immediately review their work.

If the feature must be checked by a Customer then the solution is more nuanced.
We try and send features over to clients via instant messaging as soon as they
are ready to be reviewed. This is similar to our internal approach above.
Failing that, if we need to deploy a hotfix to production we will back the
changes out with `git revert` and deploy our changes up. This is nasty, we know,
but it often encourages you to change your policy of review or open up better
lines of communication with your clients.

## Dependency on other releases

From time to time we work with other teams to deliver software. We try and
integrate into a single team where possible working on the same codebase.
However we have dealt with situations where the other team is delivering an
API that our team will have to interact with. Often we know the spec of the
API before it is built so we can mock it out. Problems arise when a change to
an API occurs and we update our code but the API side has not implemented the
change yet. A deployment to production would mean miscommunication with the API.
This is a blocker.

Another variation of this is migrations not being run at the same time of
deployment. If you push your code and it tries interacting with fields that
do not exist yet you're going to have a bad time. Another blocker.

The first solution we jump to is to hack the setup. We try and get their team
to deliver the API in the same sprint and codebase as us so we can't deploy them
separately. This way we can always keep in sync. We would always recommend
running migrations on deployment and not having a silo'd DBA run them instead.
You can often convince the Ops Person or DBA to allow you to run migrations if
you promise to only commit non-destructive migrations or get them to lock down
DB permissions so you cannot drop tables, remove columns, etc.

Alternatively if we cannot deliver as a single team, we get smart. Getting smart
means using `if` statements. If this API call fails, fallback to using the older
API call. If this field doesn't exist in the database, don't render it. This can
get messy and should be cleaned up as soon as you can but it does unblock you.

Success of your Continuous Delivery practice depends on your ability to react
and unblock your pipeline whenever issues arise. Broken builds occur and that's
okay, your team needs to be drilled to respond and fix them as soon as possible.
Work in progress and work ready for review is part of the software delivery
process but too must be dealt with sensibly. Dependency on other releases should
be avoided where possible but you can get smart too. Ultimately, if you develop
a culture of responsibility for keeping the pathway clear then you will truly
start to benefit from Continuous Delivery.
