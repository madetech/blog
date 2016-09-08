# Pair Programming
We've helped a number of organisations successfully adopt pair programming, giving their teams the ability to increase productivity, improve knowledge sharing and enhance the quality of their software.

With this article/chapter, we're sharing our experiences when introducing pair programming to software teams, and we'll take you through the techniques you'll need to apply what we've learnt to your organisation.

## Background
Pair programming was first introduced as part of the Extreme Programming (XP) software development methodology, as an 'extreme' way to practice regular code reviews. Conceived of by [Kent Beck in 1999](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0201616416), XP is a collection of software principles which help teams to deliver higher quality software. It places value on communication, simplicity, feedback, courage and respect, all of which, as you'll discover, lead to a positive pair programming experience.

## How It Works
Pair programming involves two developers sitting at one computer, with one driving, and the other navigating. The driver types out the code, whilst the navigator constantly reviews what is being typed and, at regular intervals, the developers switch roles.

There are a few guidelines that you should follow when pair programming. These will help you to get the most out of your pair programming experience, and sidestep common pitfalls experienced by others.

#### Driving
The driver is solely responsible for typing and controlling the screen. They should externalise their thoughts as they type, and be sure to constantly communicate with their navigator, discussing ideas and clarifying where necessary.

One of the more frustrating aspects of being the driver is that their navigator often has much more time to think, meaning they're able to much more quickly convey their ideas, whilst the driver is concerned with typing out the right syntax. You'll often feel clumsy or slow, as the navigator will be able to spot things more quickly than the driver. This is ok and to be expected.

#### Navigating
The navigator is responsible for reviewing everything the driver types, suggesting improvements to the code being written, alternate ways to think about the problem at hand, and pointing out typos when it is safe to do so.

#### Switching
After a short period of time, to be agreed upon by the developers, the pair should switch roles to allow each person to get an equal amount of time driving and navigating.

#### Taking Breaks
Pair programming is intensive, so pairs must make time for short breaks roughly every hour.

#### Coaching vs. Pairing
Pair programming is when peers sit and work together, but it's not uncommon to see pair programming as a form of coaching, where a more experienced developer will sit with a less experienced developer and attempt to upskill and explain their rationale around particular design solutions.

## Why It Works


#### Programming Is Hard
(Quote: "hardest thing in programming isn't typing")
The most time consuming aspect of software engineering isn't typing, it's the time spent thinking about how best to solve the current problem.

#### Increase Brainpower
As the saying goes, two heads are better than one, and with two developers working on the same problem they're much better equipped to reach an elegant solution.

#### Validation Of Ideas
Pairing encourages you to explain your thought process as you go, whether you're the driver or the navigator, so ideas you have are much more quickly validated than if you were sat contemplating them alone.

## Benefits Of Pairing

#### Productivity & Focus
Working so closely with someone else means you've got no other option but to double down on the thing you're working on. Shared responsibility. Ping pong & Pomo.

#### Higher Quality
Accountability of having someone watching you write the code, harder to take shortcuts. Two different knowledge sets attacking the problem.

#### Domain Understanding
Pairing is a great way to share domain knowledge within an organisation, rather than letting one developer become the sole gatekeeper of a project.

#### Improved Resiliency
A single developer is much more likely to be distracted by interruptions, meetings, emails etc #### a pair of developers are more resilient to interruptions because it's very obvious that they're in the middle of something.

#### Team Building & Cohesion
Spending that much time working so closely with another person naturally makes developers more social #### programming is traditionally a very isolated profession, pairing makes that less so.

#### Learning
Because each developer will have knowledge in different areas, knowledge lacking in one developer is easily shared by the other.

#### Continuous Code Review
The quality of code written by pairs is much higher, because the navigator is constantly reviewing the code and thinking about edge cases.

## Challenges In Pairing
#### Switching Mindsets
As programming has historically being a solo activity, the mindset shift required to working on code together is significant. Developers often stuggle to take onboard others ideas and externalise thought processes. This can be particularly challenging if you've worked solo for a long time.

#### People & Time
Putting two developers on a task, doesn't mean it gets solved in half the time. There is therefore a cost implication to pairing, though significant beneifts like better code quality, less technical dept etc.

#### Exhaustion
Pairing is very tiring. When you've spent the entire day pairing with somebody, communicating your thoughts and working on complex problems, you'll feel like you've achieved a lot, but be exhaused from this.

#### Disengagement
Some developers will be resistant to pairing or will spent their time less engaged in the activity. If developers are checking their phone constantly, sitting back in their chair, not communicating actively, these will be signs of an individual that is disengaged.

#### Skill Disparity
You'll often find pairing works less well when you've got signifiant skill disparity between a pair. If one engineer is clearly the more experienced and the one making all the decisions, then this can lead to the less experienced feeling overwhelmed and demotivated, whch can lead to disengagement.

#### Pairing the wrong people
It's important that you pair developers which will be well suited to working together. If you've got two developers who are negative and don't see the benefits of pairing, this will create a bad pair. If you've got two developers who constantly overengineer the most complex solutions, this also leads to a bad pair.

#### Backseat Driving
You don't want a situation where the navigator is literally dictating what the driver types #### this is an indication of skill disparity.

#### Communication (Your Baby Is Ugly)
Pairs need to be able to communicate openly and honestly with each other, if one has an idea that the other knows to be bad, they must be capable of saying so.

## Introducing Pairing
#### Getting Started
Start small, take two developers who are keen on the idea of pairing, get them to champion it, set them a task to complete and give them the space they need.

#### Trial Period
Have those developers pair together for a short while, a couple of weeks.

#### Don't Assign Pairs
Don't force developers to adopt pairing if they're not ready.

#### When Not To Pair
Not every task requires two developers to tackle it, on occasion a task will be very straightforward to complete and largely relies on muscle memory rather than significant amounts of thought.

#### Removing Blockers
##### "Double The Hours"
A popular argument for not adopting pairing is that you're doubling the man hours needed to complete a task, which is not true. You're likely to find that the number of man hours does increase, but you'll also find they produce better quality code.

##### Management Buy In
Active collaboration results in a product that is higher in quality, and lower in defects. When software projects fail, it's often because of poor communication; pair programming reduces the risk around this because you embed communication and collaboration into the delivery process.

Removes the risk around when a developer leaves, as other developers will have domain knowledge of the projects they were involved in.

##### Cynics
It's a hot button topic in software and you'll frequently find people against pairing. You can't force a cynic to enagge in pair programming, but you can get the people who are interested in pair programming to evangalise it and over time, we've found this helps to bring people around.

#### Review
As with any agile process, it's always valuable to review progress with pair programming and see whether it's working well for your organisation. There are a number of retrospectives that you can run to discuss the things that have worked well and may not have worked so well.

## Pairing Environments
#### Workspace & Equipemnt
We see the ideal pairing workstation has having two mirrored screens, plus a shared keyboard and computer. The pairs should be able to comfortable sit side-by-side with one another in an enviroment which is ergonomical. At the bare minimum, a pair should have a single computer which they pass back-and-forth.

#### Remote Pairing Setup & Tools
As remote working has become more popular, tools such as Screenhero have gained traction and are a great way to pair program from different locations. Tolls like Screenhero allow you to share your screen and let the other person drive, as if it was their own computer.

## Conclusion
Programming has become more social, through the increased adoption of open source and plethora of online tools that help software teams to collaborate. We see pair programming as being the natural evolution of this and a technique that will become more widely adopted in years to come.

### Downloadable
