# Agile Sprints: Moving as a Team

We're a company dedicated to producing quality software our clients love, and we're constantly striving to refine and improve the processes we use to do so. With that in mind, [getting things "Done done"][done done] is a massive priority for us, and anything that hinders that ability is something we will always work to remove.

On a recent project with a relatively large development team, we noticed that quite a few things were being "done-ish", but not "done done". Oftentimes those things were 95% of the way, but needed just a little more work to get it across the finish line.

Recognising this, we knew we had to rectify the situation, in a potentially drastic way.

## A little bit of backstory

As a software development company that practices the [Agile][agile] methodologies, particularly [Scrum][scrum], we continually work with clients to break their project down into stories describing a particular feature, and then we break those stories down further into subtasks.

After assigning a story point value to each of those subtasks, we agree with the client on the total number of story points we will deliver in a [sprint][sprint]. Typically a sprint lasts for two weeks, but can be anywhere between one and four, depending on the project and the client.

To monitor our progress during the course of the sprint, we use [JIRA][jira], an issue tracking tool. The stories, including their subtasks, are added to JIRA, ready for developers to come along and assign an issue to themselves to indicate that they are working on that thing. When we've begun work on a task, we move it into the 'In Development' column.

On the project in question, we'd set JIRA up to have columns representing each environment in the build pipeline: development, continuous, staging and production. Once the developer working on an issue had verified the issue in each in environment, they could then drag the issue into the next column, ready to verify it again in the next environment.

## The Problem

A few sprints into the project, what we found was that, despite progress going noticeably well, there were enough comments coming back from the product owner that we realised that certain tickets hadn't been thoroughly checked, that they hadn't been "done done". More seriously, we'd failed to complete a couple of sprints because we'd had to re-open issues and spend more time addressing comments that had been raised against them.

The whole team sat down to discuss the issue, and to find out what we could do to prevent this from happening. Two things quickly became apparent: there was a lack of any kind of code review process (we hadn't yet adopted [the pull request approach Fareed recently wrote about][pull requests], in fact, our solution acts as an alternative to that), and the volume of issues to be completed in a sprint, along the free-for-all approach to picking those issues up, led to developers allowing themselves to become distracted from making sure the issue they were working on was 100% complete before trying to move on to the next one.

## The Solution

> Individual commitment to a group effort - that is what makes a team work, a company work, a society work, a civilization work.
>
> -- Vince Lombardi

The first thing that we picked up on was the arbitrary way issues were being picked out by developers: a developer would pick an issue from a story, and then maybe something would block their progress. They'd leave the story in the 'In Development' column and then, without much discussion, pick up another issue and begin work on that.

This was clearly not useful.

What we decided was to ensure at all times that our JIRA board reflected what was actually happening, so if we were working on something locally, it was in the 'In Development' column, if it was in one of the other environments, it was in the relevant column. On the other hand, if progress had been blocked for some reason, the developer was to discuss it with the others to try to resolve the blockage, and if that still didn't help (such as when we were being blocked by external services), it was moved back to the 'To Do' column and flagged for the attention of our Scrum Master.

Another major turning point for us was to limit the amount of stories we could have "In Development" at any one time. The problem with our previous approach was that developers were tending to work in a siloed way, each of us cherry picking issues from a number of stories to the point where there could be as many stories in progress as there were developers. What we needed was for the whole team to take responsibility for each story, making sure that, when a story was started, we all go out of our way to get that story completed and verified, confidently *knowing* that it is ready to go to production.

We did two things in JIRA to help us with this:

The first was to limit the amount of stories that could be "In Development" to 2. If we went over this limit, JIRA would paint the column a nice deep red to make sure we were aware we'd crossed into the danger zone. Each story might have a number of subtasks, which usually meant there was plenty of work to go around when beginning a story.

The second thing we did was to add a "Verified" column. On this project, deploying to production regularly wasn't a luxury we had, so we had to know that what was in staging was at least production ready. The rule with the "Verified" column was the developer assigned to the issue was not allowed to move the issue into this new column, they instead had to get independently verified by another developer.

The benefits we noticed from implementing and strictly adhering to these two rules were immediate and massive.

One of the first things to happen was that there would be a pair of stories (meaning we were at our 2 story limit) with several subtasks, enough for everyone to go away and work on. Some of those issues would naturally require less time/work than others, so the developer working on such an issue would now be unable to pick up another issue in a third story, as the initial two stories had yet to be completed.

This directly led to a huge increase in the amount of [pair programming][pairing] we were doing; suddenly each developer was invested in getting stories they might never have worried about over to the "Verified" column, so that they could progress onto the next story. With a second set of eyes on the issue, pairing meant we were able to move much more swiftly through a story and whilst ensuring the quality of the code being written.

Pairing wasn't always the solution though, and the other effect these rules had was on instilling a sense of urgency that wasn't necessarily present before.

We now were communicating much more regularly to check where everyone was on a particular issue, with a view to getting that story completed. Skype/IM messages can be ignored, so we communicated verbally to make ourselves heard. It meant we had a very active forum in which to ask for help or raise concerns if we had them, and when we ran into a blocker out of our control, we would make the decision to put the whole story back in the "To Do" column until it could be resolved.

Ultimately what happened was that we moved much faster, as a team.

It bears mentioning that there were instances where the 2 story limit was simply too low, such that we had to begin work on a third story out of neccessity e.g. when one story's issues could only be handled by one particular developer (in this instance the only one of us with any knowledge of a specific .NET application).

In exceptional circumstances like those, the limit must be broken for progress to continue to be made; the "In Development" column will turn red for all to see and feel pressured by. I'm not suggesting more pressure is a good thing, but there's a palpable sense of relief when the column turns back to its original colour and we know we're not breaking our own rules.

## Wrapping up

The takeaway for you, the reader, is that it may be worth introducing these two rules to your projects:

1: Limit the amount of stories you have in development at any one time. The exact number will naturally vary according to how big the size of your team is, but we'd suggest no more than 4.

2: A story can't be closed until all the subtasks within it have been verified, and a subtask must be verified by someone other than the developer(s) that worked on it.

Smaller development teams of 2 or 3 developers might not feel the benefits of this approach, in which case adopting the previously mentioned [pull request method of code review][pull requests] might be the best solution. On the flip side, individuals in larger teams are likely to benefit from increase in productivity, communication and, most importantly, the sense that they are *part of a team*.

--------------------

[done done]: https://www.madetech.com/blog/getting-things-done-done
[agile]: https://en.wikipedia.org/wiki/Agile_software_development
[scrum]: https://en.wikipedia.org/wiki/Scrum_(software_development)
[sprint]: http://scrummethodology.com/scrum-sprint/
[pull requests]: https://www.madetech.com/blog/pull-requests-and-continuous-integration
[pairing]: https://www.madetech.com/blog/pair-programming