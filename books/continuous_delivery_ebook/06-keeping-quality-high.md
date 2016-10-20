# Keeping quality high in your Continuous Delivery pipeline

Practicing Continuous Delivery is worthless if it's not to facilitate the delivery of high quality code. In this article I am going to cover some techniques, tools and best practices we employ at Made keep our pipelines moving, and how you can compel developers to push quality code often by rewarding them for attention to detail, while not punishing them for making mistakes.

## One change at a time

The most typical development process is making a change and testing it. Making another and testing again. Even the most complex features of an application grow from simple code. Employing this technique of incremental development is rewarded in many areas of software development. Best version control practices typically involve breaking large changesets into a series of small updates. These atomic, self contained commits are readable by themselves, and thus easily understood, so shared understanding of a project doesn't get lost in a slew of massive isolated updates.

Like a grand painting, complex mechanics and fine details emerge from small additions and deletions. A 1000 line changeset is difficult to fully comprehend and give feedback on, whereas few lines of good code rarely is. Large changes result in less shared understanding of a feature, and a lower chance of being improved. Small changes are easy to store in your head and thinking of ways to improve them is simple. If people can easily understand other peoples changes, they are more likely to make suggestions. If they can't, they'll leave it and assume it works fine.

Small changes are largely beneficial in continuous delivery. If you push one small commit to master and the build breaks, it's easy to work out where the bug was introduced. Better yet, if your change is just a few lines of code, it will likely be trivial to work out which bit went wrong. Long lived branches with large changes, on the other hand, can easily become out of sync with master, creating conflicts which can lead to hairy merges. Continuously pushing to master means your new code doesn't lose the context of the project as a whole. It's embedded in the branch that's going to production, the more regularly the better.

## Keeping it together with tests

You've made a change in one part of your application to fix a bug, and it's caused a bug somewhere else to spring up. Maybe an old bug you thought you'd squashed, or something entirely new. You've probably experienced this before, this is very common when developing complex applications, and can unfortunately be easily missed. Without a robust test suite, including unit tests which ensure your business logic is sound and feature tests which ensures the user can actually use every part of it, mistakes like these can easily be missed, and buggy code can leak out to production.

At Made we believe testing should come early and often. Not only do we normally employ TDD, meaning continuously testing throughout development, but we run tests in the 'build' step of our pipelines, meaning it has to be run before we can deploy any code. If tests fail, the code can't be deployed. The primary benefit of this when practicing continuous delivery, and small atomic commits, is that problems are discovered very quickly. Having a robust test suite which ensures the reliability of your product after every change means you can develop without fear of breaking anything. Running tests after 40-50 commits and having them fail may give you hundreds of lines of code to parse through to find where the bug was introduced. If every commit to master is tested, then bugs introduced in a commit of a few lines can be found **quickly**. Better yet, fixing them is cheaper early in development than it is when the feature has reached production, and quicker fixes means more time for the fun parts of software development.

Testing so frequently has its consequences, however. Test suites are slow. As projects grow, you can see your test step grow from seconds, to minutes, even to hours on very large projects, which is clearly a frustrating impediment to shipping continuously. You want the time between development and production to be as short as possible. There is no canonical 'fix' for this, for many it is what it is. Some developers, however, advocate only testing new code and crucial areas of your codebase in build steps, for example the checkout process of an e-commerce store. This means bugs can still appear and get missed, but it also dramatically reduces the amount of code which needs to be tested, speeding up your build step and reducing your time to production.

Pushing frequently can alleviate some of the pain of all this, however. You can push code and continue working, and only stop when you notice the build failing. The tests can just run in the background, frequently enough to alert you when something goes wrong, but not demanding so much of your attention that you can't get other work done asynchronously.

## Stay beautiful

The easiest projects you've ever worked on are the projects which had consistent, readable code. Any developer can work faster by writing ugly code, and still have it work beautifully and efficiently, but as soon as somebody else comes along the work suffers. The pace is slowed as they come to grips with it. Finding a bug, or the right places to implement something new, becomes much more time consuming.

Maintaining readability of a project is paramount because projects which are easily understood are easy to work on. Developers can become familiar quickly and ship faster. An app's source code is a manual for future developers, the code you write will become the standard you and others will follow when working on that project - and even future projects - so it behooves you to follow best practices at all times. So if we use automated tools to codify conventions we like, and test every revision of a project against them, sloppy work is more difficult to get through the pipeline. At Made, we use a number of tools on every 'build' step of our deployment pipelines to ensure the code passing through is of a high quality.

For example, as one of the first steps of a Ruby project's build step, we run [Tailor](tailor) and [Cane](cane), which are static analysis tools which review the style of every Ruby file in the codebase against a set of rules we define. Tailor checks the cosmetics. Is the whitespace correct? Are method names all in lower-snakecase? It checks that the code in our project matches our own guidelines.

Cane checks the complexity of code. For example, by using an ["ABC" metric](abc) which analyses how much a single method is trying to achieve, we can ensure the methods we're writing and using make sense by themselves and follow DRY conventions. In JavaScript we use [ESLint][eslint], a newcomer to the linting world. Like Tailor, it checks our JavaScript code against defined rules, and supports languages which transpile to JavaScript, for example React's JSX syntax.

Fixing these syntax issues and accidental complexities as they come up is really helpful. Even if you're just pushing a hotfix which is a few lines long, ignoring the quality of that code to speed up development would allow the codebase quality as a whole to suffer. Your code will crumble brick by brick unless diligently maintained. Preventing bad code from entering production forces the codebase to maintain a good shape, and although this may slow developers down in the short term it improves productivity in the long term.

[Brakeman][brakeman], a Ruby 'vulnerability scanner', is the fourth tool in our static analysis arsenal. We use to in our builds to check for potential exploits our applications may be open to, so we can cut them off before they reach the wild. Although a tool which relies solely on static analysis and generic assumptions can't catch every possible point of attack, knowing that we're safe from common or simple exploits after a short build time is good for peace of mind.

See [our post on code quality](code_quality_post) for more on tools you can use to keep your codebase happy.

## Fail like a pro

"Breaking the build" is often dreaded, but if we consider all of the ideas discussed in this article to be valuable, then actually preventing code which is broken, unsafe, or just plain ugly from getting into production is a very good thing. Fixing problems quickly as they come up actually speeds up development as a whole and ultimately encourages developers to get it right the first time. To take their time in developing new features and make sure they're as good as they can be when they're pushed. By developing with this framework around your deployment process, there is little fear of accidentally pushing code which could harm the customers experience, the experience of future developers, or our own experience working on a codebase. Code which isn't good enough gets rejected, and you fix it.

This has a positive side effect of preventing other developers from stacking code upon broken code. The team is all aware that some part of the codebase is currently unreliable and leaves it up to the original developer to sort out, before making changes to the same things.

## Be happy

Ultimately, many of these tools and use cases focus on ways to get developers working well together, following agreed best practices and conventions, taking time on their work and continuously receiving feedback on what they've achieved. This attention to detail makes us proud of our work. This process encourages developers to shepherd their changes to production, rather than throwing them in the wind.

Giving responsibility to developers makes them care about the quality of the code. They care about helping the customer, they want to see it being used and appreciated. Furthermore, by deploying regularly while keeping quality high, any small fixes needed once a feature hits production can be picked up by the developer best suited for the job. If they have been waiting days or weeks for a deployment, they may no longer be able to get around to fixing small issues quite as quickly. A back and forth discourse emerges whereby changes can be requested and implemented quickly.

Tests, QA, feedback and linters all on their surface slow down development. But in the long run, they provide a safety net for creativity and experimentation, which results in better, more stable code and happier developers and customers. They are an important part of the virtuous cycle continuous delivery tries to achieve.

[code_quality_post]: https://www.madetech.com/blog/there-is-more-to-code-quality-than-coverage
[tailor]: https://github.com/turboladen/tailor
[cane]: https://github.com/square/cane
[abc]: http://c2.com/cgi/wiki?AbcMetric
[brakeman]: http://brakemanscanner.org
[eslint]: http://eslint.org
