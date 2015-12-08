# Preparing your team for continuous delivery
    - Introduction
    - The art of sneaking it into production undetected
    - Communicate with commit messages
    - Developer Confidence obstacles
    - Production awareness
    - Big bang deploys are your enemy
    - Summary

## Introduction

  It can be challenging to get sufficient infrastructure set up to enable you to practice continuous delivery, but the biggest challenge may be changing the way you (and your team) think about releasing software.

  The goal is to evolve software in small increments, not to drastically change it all at once. This has been proven to make releasing software faster, more reliable and easier to debug.
  Each contribution/commit has to be releasable. There is no two ways about it.

  This may sound unreasonably optimistic but it is possible, people are doing it, and you should be doing it.

  Releasing to production should be boring. So boring in fact that there should be no need to notify anyone that you are doing so.
  If someone has a commit in the pipeline that should not be deployed to production without further work, then you are not doing continuous delivery.

  If a team member has introduced a bad commit, it is up to that developer to fix it. If this starts to block the deployment pipeline, the commit may be reverted.

  Developers can be reluctant to adopt such a drastic change of pace, but once you have experienced the benefits you, and your team will never look back.

  It is vital that every single member in the team be on board with this style of working or it will fail.

  I personally fell in love with continuous delivery even before I knew what the term meant. It happened naturally in an attempt to deal with the anxiety of massive deploys.

  Below are some guidelines that must be followed by the entire team in order to successfully practice continuous delivery.

### The art of sneaking it into production undetected

  Production is the one and only source of truth. By proving that something works in a non-production environment does not mean that it works.
  When you work on a feature, aim to get 99% of it deployed into production undetected, by the customers, users, and the rest of the code in the system.

  This is also known as Dark Launching and you will be doing a lot of this.

  Sometimes dark launching can be achieved by something as simple as omitting a hyperlink to a page, sometimes it is more complex, but it is never impossible.
  Feature flags may be used when dark launching becomes too complicated, but should be treated as a last resort.

  Some of the software giants such as Google and Facebook (to name but a few) have proven that these techniques work.
  These companies move at a rapid pace, and their developers commit straight into the master branch.

  Your new feature needs to be designed in such a way that it can be activated through a simple trigger.
  Decouple it from your system as much as possible. This should be one of your highest priorities in producing modular decoupled code anyway.

  The last 1% of code that you push up is usually just the trigger that makes an entire feature live to the public.

  By getting your code into production early, it has proved to some degree that it can co-exist with the rest of the system, and that none of the other existing functionality has regressed.

  You will find that your definition of done shifts from some pre-production verification to actual production, because it has become so easy.

## Communicate with commit messages

  When writing software, having fast descriptive feedback can make all the difference.

  Continuous Delivery demands that you integrate your changes with the master branch frequently.
  I see no reason that you cannot commit to the master branch atleast once every hour if you intend to keep the code.

  If a developer has not committed all day, there is no way of telling how his work will fit in with the rest of the system.
  Frequent commits mean that you have considered the bigger picture and that you have broken this down into smaller, more maneagable sub-problems.

  As a positive side-effect of this team members get a lot of feedback on the current state of the project.

  You quickly discover misscommunications or people heading in the wrong direction with their intended solutions.
  In big teams this becomes vital. Merge conflicts become less frequent and less complicated to solve.

  Publish your commits to your chat room, or put them up on a big screen for all to see.

  Good commit messages matter, and your master branch must remain pristine at all times. A good understanding of your version control system is necessary.


### Confidence obstacles
  As soon as you decide on a direction to take on solving a problem, you better be sure there are no dead ends down the line.

  There can be a lot of pressure around making these decisions early on and being confident that they will be right.

  At times there may be missing or incomplete specifications that will require your system to adapt at a moment's notice.

  This prevents some people from pushing small commits often. They are uncertain whether their intended solution is indeed the correct one.

  Practicing continuous delivery generally encourages you to clarify your intentions before you start writing large amounts code.

  As soon as the first commit goes in, everyone can see it and it can generate feedback which would benefit the overall project.

  I have found that this also promotes the quality of code as small chunks are easier to analyse by other team members, and there is no hiding bad code in thousand line diffs.

## Production awareness

  When developing new features it is vital that you have considered all the factors for releasing it into production as soon as you start work on it.

  This may even change the way you approach the problem at hand, which is a good thing as the only end goal is your production system.
  Sometimes this means pulling down real production data and running your code against it for verification.

  Beyond that I am going to assume that you have battle tested your feature as much as possible in your staging environment and your automated tests prove, to a certain degree, that it is correct.

  If you have something like a [blue/green](https://www.madetech.com/blog/a-guide-to-blue-green-deployments-and-going-live-every-day) or [canary release system](https://www.madetech.com/blog/canary-releases), it makes it much easier to verify the actual production system by running the actual code.

  Assuming you do have a zero downtime deployment system, you generally are forced to share resources between the different versions of your application.

  The real obvious one here is the database.

  When we implement new features, we are required to clean up tables and alter schemas. We keep our codebase tidy and do not allow dead code to exist.
  At times when practicing continuous delivery, it makes sense to hold off on certain cleanup tasks until we are absolutely certain that no previous (potentially live) systems depend on this data.

  You must develop the foresight to never negatively affect your running production system.

## Big bang deploys are your enemy

  Big bang deploys mean releasing a large amount of code into production at a time. This usually happens on a Friday afternoon because a deadline has forced you to do this.
  If it were not for the deadline who knows how much code would have accumulated for the release.

  It can be complicated and developers can experience a great deal of anxiety when deploying features to production.

  Introducing thousands of lines of code into a running system can have unexpected consequences. It is hard to know exactly what went wrong, and it can be difficult to diagnose.
  Large faulty production deploys are also difficult to remedy as you cannot roll back easily.

  Small commits are easy to reason about. You get instant feedback on the quality of your small change as soon as it is released.
  Should something go wrong, you only have a handful of potential suspects to debug.

## Summary

  Whenever you write a new piece of code for a feature, consider the earliest point at which it makes sense to commit it in.
  Even if it's a small schema change, send it up to production and be done with it.

  Constantly evolve the current system, and don't try and introduce large amounts of new functionality at once.

  Above all, Continuous Delivery means having the discipline to stick to these principles even when it is difficult to do so.
