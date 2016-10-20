# The benefits of Continuous Delivery
# The business value

Continuous Delivery is a technique that grew roots in the IT department, but is very much focused on delivering value, in the shape of shipped software, back to the business more frequently and more reliably.

We, as most modern software companies, focus on delivering Software as a Service over the Internet. While we expect that you're able to realise many of these benefits if you're delivering software via another mechanism such as application installs, there may be some areas where your ability to move at an 'as a Service pace' might be reduced.

There are a number of reasons we believe organisations who take software delivery seriously should be investing in Continuous Delivery.

## Faster to market

The primary business drivers we see behind Continuous Delivery adoption is that it both facilitates and encourages shorter delivery cycles.

Continuous Delivery practitioners must be integrating their work with the rest of the team at least once per day, and ideally, a couple of times an hour.

Continuous Delivery can encourage stakeholders across the organisation to start thinking of software delivery as a series of smaller features. The demands of keeping a single software product release-ready without making use of patterns such as feature branching, are made trickier when delivering particularly big changes.

By releasing small features more regularly, software and the value that it's intended to deliver gets in to the hands of customers faster. We see that the sooner you can get software to customers, the sooner you can start getting feedback, and the less time you spend working on unnecessary or less valuable features.

As more organisations adopt fast release cycles, we're seeing customers expecting this as the norm. Businesses such as Slack, the team communication tool, make much of their "What's New" feature, which highlights the changes that have been released in the past day.

## Improved engineering practices

We've observed Continuous Delivery as the catalyst for improving development practices through the delivery cycle, from project inception through to maintenance.

The need to keep software release ready encourages, and some corners may argue, demands the adoption of good software engineering practices, such as Test- and Behaviour-Driven Development, Pair Programming, techniques that we believe, over the course of a software project, will increase your ability to move quickly with confidence.

When the business demands more regular release cycles, technology teams are incentivised to leverage higher levels of automation. With more regular builds, resource intensive manual QA processes should be replaced in-part (or ideally, in full) with automated UAT suites. Performance testing and the associated provisioning of infrastructure can be automated, similarly with security testing.

## Reduced risk

Big releases containing many changesets, perhaps in extreme cases, the culmination of many months work, offer significant risk. Our experience tells us, the larger the deployment, the more likely something will go wrong.

By contrast, we see that releasing little and often keep changesets small, and accordingly, the risk of the change introducing issue is reduced.

In addition, by practising deployments more regularly, we become better at them. We feel the pain of bad deployment practices more regularly, we're better incentivised to replace manual steps with automation, and so the risk associated with human error becomes a less likely occurrence, and releases become a less resource intensive practice.

Where it allows, our general principal would be to not be overly scared of acceptable production bugs to the detriment of moving quickly. Where software is released close to it being built, resolving issues is generally made easier as memory of the implementation is fresh. When coupled with a fast, automated pipeline that allows followup fixes to be released quickly, issues can often be squashed before they're even noticed.

## Releasing is a business decision

We see too often that releasing software updates is a technology-lead decision, rather than a commercial decision.

In many organisations, releasing is a process encumbered with risk and involves a highly orchestrated series of manual steps, each of which offers an opportunity for error. A good Continuous Delivery environment replaces these manual steps with automated tooling.

By encouraging discipline within the team to ensure software is always in a release-ready state, the decision to release new features and updates can be moved back to where we believe it belongs: with the commercial stakeholders.

In particularly mature Continuous Delivery teams, an organisation can go as far as empowering Product Owners to physically push the button to make a release whenever they're happy with the changeset, in a complete absence of operations folk standing by in support.

Beyond this, teams can move a step further to practicing Continuous Deployment. In a typical Continuous Delivery setup, full automation usally happens as far as a staging/pre-production environment, with a manual button-push to trigger the production release. Continuous Deployment fully automates this final step, so that a code check-in that passes all previous steps in the pipeline will be automatically deployed to the production environment.

## Expose inefficiencies

We often find the adoption of Continuous Delivery to be a strong tool in exposing inefficiencies through the software delivery process, from insufficient requirement description, to unexplainable change control processes.

By tightening up discipline and tooling around the build and deployment process, and particularly by focusing on delivering incremental release-ready features, the true barriers preventing an organisation from moving fast are highlighted with a big red pen.

In many cases we see that outdated technology practices can be a strong force in preventing software being delivered in an acceptable or ideal timeframe for an organisation. However, as more businesses realise that they're actually software companies in disguise, there are many factors outside of actually building the software that can hold businesses back. By getting the software delivery process right, an organisation loses the most obvious reason for slow software delivery, allowing it to focus on fixing wider issues.
