# Keeping quality high

Code quality is a term that is often thrown around in the software engineering industry. And like the art of coding itself, it is very subjective and it's true meaning will differ depending on an individual, or a team's beliefs. But at its heart most engineers and teams would agree that good quality code is easy to read, well tested, and maintainable in the long term. But how do we achieve this?

## It starts with a feature

Often a client will present what they see as the solution to a problem, guised as a feature request. However when a team takes their first slice into this feature, they should not do so blindly.

If there are big questions about functionality,  or end-user requirements, these unknowns should be uncovered.  This will enable the team to build a better solution, with the least amont of code possible. Ultimately, this alone will increase code quality; less code means a smaller codebase which leads to a more managable system in the long term.

From the outset understanding the shape of a feature keeps the team laser focused, meaning everyone has a clear definition of success for a task. Although an initial slice may have been defined, teams should not be in fear of changing it's requirements if during the course of an iteration they find a cleaner approach.

## Next we commit

At Made Tech, we use pull requests on all of our projects, meaning we work on new code in a separate branch and request review before merging it and releasing it. We deliberately keep changesets small, releasing small increments of the feature early and often. We work this into our version control and code review workflow in a practice we call "Single Responsibility Pull Requests".

This practice avoids "Big Bang" deployments, where many changes have been made since the last production deploy, introducing many points of potential failure, rather than just one. Releasing continuously hopefully means our pathway to production is always clear. This is a fundamental principle behind [continuous delivery](book).

Furthermore, smaller changesets are easier to digest, so when we request code review, reviewers are able to do a better job. They have more room to comment on particular areas, asking questions or suggesting improvements, if they only have to look over 10 lines, rather than 100. We can be sure that they properly understand the code we've implemented if they only have to look at a small chunk. Many changes over many files with many concerns can get confusing. The reviewer doesn't necessarily know what all the parts do and making sense of the whole thing can be intimidating. Massive cognitive overload leads to poor reviews. Poor reviews leads to bad code getting into the codebase, reducing quality.

Make sure you break large features down into smaller slices. Write these in a way that they can be deployed individually rather than as a massive chunk whenever possible, and don't block the route to production. Request code reviews continuously during development to ensure reviewers can understand the feature throughout, rather than trying to make sense of it at the end, and always make sure they're satisfied before merging it.

## Raising the bar

Keeping code quality high through manual code review is great and a really worthwhile practice, but it is often not so good for static code analysis. Static code analysis is another vital way we at Made Tech keep our code quality high, and machines are much better at doing this than humans.

Static analysis can be broken down into a number of areas like complexity, style and security, and there are many tools that deliver this functionality. For raising the standard of your codebase the primary focus should be ABC complexity.

ABC complexity is counting the number if assignments, branches and conditions within a method or function. A high ABC metric is a good indicator that the code is doing too much and should be broken down in to smaller, easier to understand chunks. Its important to stress that keeping ABC complexity low doesn't always mean you have an easy to understand codebase. The metric also doesn't reward terse code, instead it prefers simple code.

Arguably our most favoured practice at Made Tech is TDD, test driven development, which is writing tests before writing code. This has broad benefits across code, but especially code quality. Like having a defined objective for a task, TDD keeps you focussed on accomplishing it, and ensures you're not writing perfunctory code. Every line you write is necessary to bring the feature closer to completion. This not only ensures you're writing the _right_ code, it ensures the code you write is maintainable over time, preventing regressions down the line. Engineers in future don't need to be afraid when making changes the codebase if they're confident that it's well tested. They can trust that if they break anything, the test suite will fail, and they'll be able to fix it _before_ it gets into a production environment. To accomplish this we include an accompanying test in every PR.

## Keeping it high

We are committed to our projects and maintain them diligently over their lifetime, so it is in our best interests to invest time in quality. Although ensuring projects start off properly is paramount, making sure they stay in good shape and quality remains high is even more important, so we employ a number of practices and tools to enforce standards over time.

One way we do this is through style linting. Style linting is another form of static analysis that requires your code to be written in a certain way, as predefined by either a lauguage, or an opinionated community standard. For example at Made Tech we use StyleLint, ESLint, and Rubocop among others.

This means over the lifetime of a project the code can only be written in a certian way, so it will stay consistant. Often linters will often suggest better ways of doing things, progressively upskilling the team in a language, the is extremely helpful when onboarding team members who are less familiar with a language. It also makes people feel they are delivering high quality code whilst still learning.

However style linting should not be seen as a silver bullet, as it doesn't always lead to high performant code. Sometimes asthetics have to be sacrificed for efficiency. Additionally style configuration is highly subjective. At the end of the day it comes down to an individuals beliefs. People in the same team may have different ideas about how code should look, and you may even rely on third party defaults for code style rather than defining your own. What's important is that code remains consistent.

Forcing developers to run all these code quality tools themselves can be a drag, but we want to ensure they're always run before code is merged in, so we automate their inclusion in our workflow. We use PaaS services like CircleCI to automatically run our test suites, static analysis tools and security testing against commits and pull requests in Github. This means code reviewers don't need to worry about these elements, as they have to succeed in order for the PR to be eligible for merging.

Additionally running the quality assurances facilitates an engineers apporoach to code continously improves. Spotting failures due to bad looking code soon becomes second nature. This then has a benefit that as they maintain the project as they encounter new areas of the project they are able to bring that code upto scratch. A process we internallty call Boyscoutting. Essentially, code should not be seen as sacred and while an engineer can be protective of code they have written they should also not be afraid of deleting or even replacing code when the time comes.

Like codebases, teams should also be ever changing as this also leads to greater code quality. A fresh set of eyes will spot problems and encombant engineer will just live with, if they have noticed them at all. Keeping the team diverse leads to greater insight.

## Conclusion

First and foremost, a well tested, easy to read codebase is easy to maintain. Employ automated quality tools to ensure the code your team writes today and the code they write next year is excellent. Deliver features one chunk at a time to ensure code review is diligent and comprehensive, without demanding high cognitive load. Write automated tests and run them on every change to prevent against regressions and let your tests document functionality, rather than trying to maintain documentation that can go stale.

Engineers often consider code they wrote last month the worst in the world. That will probably never change, as engineers we're always learning and improving. However if quality is always kept high, whilst beliefs may change, we can always be proud of the code we have written.