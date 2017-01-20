# 9 Techniques to Improve Software Quality

Most software systems will suffer from a deterioration of quality over time. Codebases become bloated, software is changed to solve problems nobody knew existed when it was initially written, and the cost of change keeps increasing.

Of course, it doesn't need to be this way, though conscious action is necessary to avoid software systems from deteriorating over time.

Here we provide 9 techniques that we've implemented in a number of organisations to help ensure that the code quality of software applications increases over their lifespans.


## 1. Beware the bit rot

Bit rot, also known as code rot, software rot, software decay, and other similar terms, is the observation that software appears to rot over time, even when no changes are made to it.

Software doesn't run in isolation, it's reliant on physical hardware, an operating system, libraries, and often, some third party services that it talks to. If it's a web application, it's going to be delivered via a web browser on a client machine, of which you often have little or no control over.

The environment in which the software runs is constantly evolving. It is therefore realistic to expect that some ongoing efforts will be needed to ensure the software keeps pace with its environment.


## 2. Don't throw software over the wall to a 'maintenance team'

Many organisations split their engineering teams, choosing to have more experienced engineers working on the tricky greenfield products, who then throw their wares over the wall to a less experience maintenance team.

A structure such as this is likely to result in a reduction of quality over time, both in staffing a team with less experienced engineers, and in the removal of any sort of ownership.

A model we've found to work better involves pulling together teams with differing levels of skills. More experienced engineers often enjoy the opportunity to mentor less experienced team members, and it ensures that experience is spread equally among teams.

If the nature of the maintenance work on your product suite means that you feel more experienced engineers aren't delivering enough value in delivering this work, it's worth considering how the work can be changed. If there's lots of manual, repetitive work in maintenance - can your maintenance team build tools to automate this?


## 3. Peer review all the things

This applies not just in relation to software in maintenance mode, but software delivery in general. We'd heartily recommend moving to a pull request type workflow where changes through the whole lifecycle of a software product are reviewed by another team member.

Ensuring another set of eyes is present on every change can help catch issues sooner, and can encourage healthy discussion on the best way to achieve code-level objectives. See also: [pair programming](https://www.madetech.com/blog/pair-programming).


## 4. Use automated code quality tools

Using automated quality tools to keep an eye on every change ever made to the software:

- Linting tools are useful to keep styles consistent. Code with a consistent style looks better maintained, and can help steer developers from being tempted to hack a quick fix in
- Automated testing can be used to spot regressions in existing features as soon as a change is made
- Code coverage tools can provide a caveated metric as to whether your testing efforts are tailing off
- Duplication detectors can help to identify where the same block of code is used in multiple places in the application, hinting that a refactor may be warranted


## 5. Think of Products and not Projects

Too often people consider software delivery as a project. At the end of the project the software system will be 'done' and barring the odd bug fix, no further work will be necessary.

Very seldom is this the case. There are [a number of studies](https://pdfs.semanticscholar.org/7eee/629b22cd3db63296cac13a0c37cb0a7235f6.pdf) that show that more often the bulk of the cost of a software application is borne in 'maintenance' - the period after the initial launch.

We'd recommend adopting a [Product mindset](https://www.madetech.com/blog/products-not-projects) to your software deliveries - shipping small, incremental improvements often, rather than fixating on a drop-dead shipping date for Gold Master Version 1.0.


## 6. Be prepared to invest

Building on the Product vs. Project point, you should be prepared to invest in maintaining your software through its life. Not just in adding new features and fixing visible bugs, but in providing enough capacity to allow engineers to continue to evolve the technical architecture of the software system to meet its current needs.

While this may result in increased operational expenditure in the short term, it removes the need for larger capital expenditure events when software systems reach a point where they need to be replaced rather than evolved, due to a lack of upkeep.


## 7. Know when to refactor

As an application evolves, you'll often see new features added, the introduction of entirely new capabilities, and improvements to existing functions.

Often the scope of an application can change far beyond its original goal. With this in mind, it's important to be able to make well informed decisions as to when to refactor areas of the application, over forcing new behaviour on top of existing features.

Refactoring may involve extracting out parts of a software system in to a new component or new software system, or replacing a part of the system that is no longer fit for purpose.


## 8. Keep on top of technical debt

Technical debt is a normal occurrance of just about every software development project. At times it is the right course of action to cut a corner to achieve a short term aim.

That said, in aiming to improve the quality of an application over time, it's important to stay on top of the debt. Engineering teams should be comfortable in prioritising the pay-off of technical debt as often as necessary. And Product Owners should be open to debate in pushing down the priority of new feature development to facilitate this - understanding that too much unchecked short term thinking causes significant harm in the long term.


## 9. Monitor the application in production

Monitoring the application in production can provide useful insights in to how the application performs in the real world. It can help identify common error conditions, and can highlight areas of the application that are less performant.

Correlating a deterioration in either of these metrics to a change in the software can be a useful thing to catch early, allowing a fix to be issued.


## Summary

Avoiding deterioration of software quality over time requires a conscious effort, both on the part of the Product Owner and the engineering team. The mindset should be shifted toward an ongoing product investment, rather than an upfront big-bang project delivery. It's important to ensure a sufficiently experienced team takes responsibility for ongoing engineering efforts, and to take a mature approach to paying off technical debt and refactoring as often as possible.
