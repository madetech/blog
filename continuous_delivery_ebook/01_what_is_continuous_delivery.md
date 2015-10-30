# What is Continuous Delivery?

The singular principle at the heart of Continuous Delivery is that the code being written can safely be deployed to a production environment at any time, and _is_ deployed as often as several times a day. These small, incremental changes allow us as developers to be confident that the code we release is stable, rather than waiting weeks to deploy huge, potentially damaging changesets.

## Where did Continuous Delivery come from?

In a nutshell, Continuous Delivery was borne, many eons ago (i.e. within the last twenty years), out of the frustration of developers stuck in what was known as 'Integration Hell', the point at which the code you've been working on for the last few weeks meets the code that the rest of your team has been working on in that period, and the point at which you realise those two code bases are incompatible in subtle ways.

It used to be that a project would be worked on by a team of developers who each went away work on their own area of code for periods of weeks or even months at a time, after which all of the work would be brought together, and everyone would knowingly walk into Integration Hell.


### Smoke Tests

Developers are problem solvers by nature and, as a huge pain point, this was a problem that very much needed to be solved. One such solution was [Steve McConnell's 'Daily Build and Smoke Test'](http://www.stevemcconnell.com/ieeesoftware/bp04.htm), from 1996. His idea was for all code to be tested at the end of every day and run as a 'smoke test'. If anything broke, chances were that it would be much simpler to fix something that had cropped up in the last 24 hours than it would have been had the test been once per month.

McConnell was an employee of Microsoft at the time, which is where that idea was put into practice. However, in the world of open source and at around the same time, Kent Beck was developing a methodology known as ['Extreme Programming (XP)'](https://en.wikipedia.org/wiki/Extreme_programming).

### Extreme Programming

The thinking behind Extreme Programming is to place an emphasis in development on best practice and, as such, it encompasses a broad range of development practices such as test first development, [pair programming](https://www.madetech.com/blog/pair-programming), and the ability to respond quickly to changes in requirements as they occur.

Where it relates to Continuous Delivery is in how it promotes the idea of [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration), which, put simply, is the process of a team of developers regularly (i.e. several times a day) reintegrating their work with that of each other and then continuing their work from the amalgamation.

The process doesn't altogether prevent integration problems, but it does mean that when they occur they are usually small enough to prevent another trip into Integration Hell.
