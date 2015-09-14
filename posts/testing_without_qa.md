Testing without QA
==================

We have an almost continual dialogue on how to improve the quality of the software that we're involved in delivering. One of the conscious decisions that we've made is that we don't make use of a dedicated QA or test role.

That's not to say that we don't believe in testing software, or in the value that a strong tester can bring when embedded in a team. However, we do often see a number of common challenges when leveraging a dedicated test role. I'll share a handful of things you should be mindful of, should you be considering bringing a tester on board, as well as some of the techniques we use to keep quality high without a test role.

## Common challenges with a dedicated test role

### Decrease in development quality

We've often observed that there's a steady reduction in development quality when a tester is brought on to a team. By having the comfort of a safety net between a commit and production, there can be a subconcious relaxing of development standards - perhaps not considering edge cases, or bothering to fire up another browser or device to run a quick test.


### Increased cycle time

There's a well cited cost of defect graph or matrix that has been doing the rounds for decades in software engineering circles. Effectively, it'll show you (very crudely) something like:

<script src="https://gist.github.com/chrisblackburn/af09e36919172f149e2c.js"></script>

As soon as you've got a second party involved in the feedback loop, the cost, or time, is increased by several multiples than in cases where the originating engineer resolved the issue as part of delivering the feature. Push the defect closer to production, the cost keeps on multiplying.


### Externalised testing

While it might be cheating to bring up externalised testing in a post that is predominantly dealing with embedded testing, we can observe cases where embedded testers can create externalisation issues.

If the testers aren't involved in both feature planning and subsequent discussion that happens during implementation, a significant overhead can be added to your engineering team to explain how a feature is now supposed to work and to triage incorrectly opened defect reports.



## How else do we keep quality high?

On most teams, we see peaks and troughs in quality. Typically you'll have a handful of particularly stable deliveries, after which it can be easy to become complacent, gently allowing quality to drop in the process.

To avoid this, there are a number of behaviours that can be encouraged.


### Continuous Integration

Regardless of how you're performing the more human element of quality assurance, we're going to need to assume that your team are practising some combination of Test and Behaviour Driven Development, and that these tests are being executed against the codebase every time a change is committed. That's to say, that as an inherent part of the software engineering process, you're cultivating a suite of automated test that are both helping to drive the design of your application, as well as providing a useful regression suite, to keep check that the features you're building today continue to work alongside the changes you make tomorrow.


### Pull requests

Another code-level feature that we often find beneficial is to use pull request style development, particularly where the team are immature to pair programming, or where the nature of the workload doesn't necessarily lend itself well to pairing.

Having another pair of eyes check and give 'approve' the change can be beneficial. If you adopt this workflow, you need to keep on top of pull requests: not letting them linger for more than 20 minutes or so. You'd also be well advised to discourage [bikeshedding](https://en.wikipedia.org/wiki/Parkinson%27s_law_of_triviality), focusing the team on truly valuable feedback.


### Peer review

Where pull requests can provide a valuable second pair of eyes at the code level, having a second pair of eyes run through some more manual testing and verification can be equally valuable.

Where we see this differ from the dedicated test role is a subtle one. By 'troubling' another engineer or team member to help validate a feature before it's moved to a pre-production or production environment, there should be an expectation that they're going to be able to give the feature a quick tick. We observe that teams should have a low tolerance for picking up sloppiness in one another's delivery.


### Pair programming

We've seen pair programming offer up many benefits to teams. One of which is improving the quality of delivery. Having two pairs of eyes focused on solving the same problem, the differing perspectives can lead to more elegant and better thought through solutions, generally with more edge cases identified and mitigated against.



While we can, and have, seen good value in properly embedded and experienced testers in teams, we often see that the drawbacks can outweigh the advantages. Cultivating a strong culture of discipline in software teams remains possibly the biggest challenge facing engineering leads. However, we see that the dividends it plays throughout the delivery, in quality and many other areas, is worth the ongoing investment.

As a final piece of advice, we'd have a strong suggestion to be wary of outsourcing any sort of test capability - particularly if you're trying to deliver software with any kind of speed. The overhead in slowing down your delivery cycles, and the communication overhead it can place on your engineering function are seldom worth the returns - particularly if you do observe any quality drop as part of the perceived safety net.

