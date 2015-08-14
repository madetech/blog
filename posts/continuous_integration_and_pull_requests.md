Pull requests and Continuous Integration
----------------------------------------

A few months ago at Madetech the [Finery](http://www.finerylondon.com) team switched to Github. Before the move we pushed commits directly into the master branch. Commit notifications with links to the diffs would then come up on the Finery channel on our HipChat server, and members of the team could review the commits at their own leisure. There was no commitment to code review.

When we switched to Github we put in two rules for committing into the Finery project. 1) Features and solutions to tickets go into pull requests and 2) You can’t merge your own pull requests — another member of the team has to do it for you.

As with any new process, this has its cons. Pull requests slow the process down. Code doesn’t get merged in straight away if all members of the team are busy. Branches have the capacity to go stale. The pros, on the other hand, have been pretty huge.

You’d think that the biggest pro would be that it helps keep the build pipeline clear if important fixes have to be pushed through quickly, but in reality pushing into master just means that the team couldn’t push unfinished commits, or groups of commits that didn’t constitute full features. The biggest pro has actually been the ability to have a conversation around the code, inline with the actual code itself. ‘Is there a better way of doing this?’ ‘I didn’t know you could do it like this!’ ‘Can we DRY this up a bit?’, etc.

Having an extra pair of eyes on a group of commits almost always highlights things worth looking at: bugs, style issues, possible simplifications, the list goes on. It also helps to form conversations around the way we write code. It helps form culture. Knowledge is shared quicker. Bus factor is lower. 

Having someone else approve the code means that there is a shared responsibility for the feature. No one person can be said to have developed it in a vacuum. If there is an issue with the feature that needs to be fixed, both the programmer and the reviewer share the knowledge gained from fixing the issue. Both of them are less likely to make the mistake again.

The other, slightly less widely-cited benefit of compulsory code review is that if you know that someone else in the team is going to have to sign off on the code, you’ll probably write it better the first time round. You can’t cut corners. You can’t sneak stuff in. Let’s face it, this happens even in the best software teams. The very idea that a code review is going to happen on a pull request ensures a reduction of technical debt.

I’ll end with a nice little pro that I’m personally the happiest about since switching to continuous integration with pull requests on Github: it’s easy and to leave someone an encouraging note on their pull request. ‘This is great.’ ‘Nice job here.’ Sometimes it’s the little things that keep you loving the work.