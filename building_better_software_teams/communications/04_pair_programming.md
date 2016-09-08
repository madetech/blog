# Pair Programming
We've helped a number of organisations successfully adopt pair programming, giving their teams the ability to increase productivity, improve knowledge sharing and enhance the quality of their software.

As a company, we've been using pair programming for around eighteen months, and we've discovered it brings a significant number of benefits, along with one or two challenges we've had to overcome.

With this article, we'll be sharing the experiences we've had when introducing pair programming to software teams, and we'll take you through the techniques you'll need to apply what we've learnt to your organisation.

## Background
Pair programming was first introduced as part of the Extreme Programming (XP) software development methodology, as an 'extreme' way to practice regular code reviews. Conceived of by [Kent Beck in 1999](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0201616416), XP is a collection of software principles which help teams to deliver higher quality software. It places value on communication, simplicity, feedback, courage and respect, all of which, as you'll discover, lead to a positive pair programming experience.

## How It Works
Pair programming involves two developers sitting at one computer, with one driving, and the other navigating. The driver types out the code, whilst the navigator constantly reviews what is being typed and, at regular intervals, the developers switch roles. Throughout their time together, the pair constantly communicate their thought processes, allowing the other developer to collaborate and help shape the direction of the code.

There are a few guidelines that you should follow when pair programming. These will help you to get the most out of your pair programming experience, and sidestep some of the more common pitfalls we've seen teams experience.

#### Driving
The driver is solely responsible for typing and controlling the screen. They should externalise their thoughts as they type, and be sure to constantly communicate with their navigator, discussing ideas and clarifying where necessary.

One of the more frustrating aspects of being the driver is that their navigator often has more time to think, meaning they're able to convey their ideas faster than the driver, who is more concerned with typing out code with the right syntax. The driver will often feel clumsy or slow, as the navigator will be able to spot things more quickly than they can. This is OK and to be expected, and the roles switch so regularly that both developers experience the situation from both sides.

#### Navigating
The navigator is responsible for reviewing everything the driver types, suggesting improvements to the code being written, alternative ways to think about the problem at hand. The navigator should be considerate and careful to minimise unnecessary interruptions when the driver is in flow. Much like a conversation, choose the right moments to point out trivial errors, like spelling mistakes.

#### Switching
The pair should switch roles to allow each person to get a mix of driving and navigating. There are a couple of methods that are often used to determine switching frequency. One technique is time based, where the developers switch at regular short intervals. Another technique is [Ping Pong](http://c2.com/cgi/wiki?PairProgrammingPingPongPattern), where developers take turns writing a failing test case, that the other developer then has to make pass.

#### Taking Breaks
Pair programming is intensive, especially over the course of a few hours or a whole day. It's important that pairs don't burn themselves out, so they must make time for regular breaks away from pairing throughout the day. These breaks provide good opportunities to do things that might otherwise distract a developer during pair programming, such as checking emails, instant messaging, or making coffee.

#### Pairing, Not Coaching
Pair programming involves two peers of a similar skill level working together, but it's not uncommon to see some organistations use pair programming as a form of coaching, where a more experienced developer will sit with a less experienced developer and attempt to upskill and explain their rationale around particular design solutions.

There are definite benefits to coaching, but it's important not to confuse it with pair programming, as it can lead to [backseat driving](#backseat-driving), and the less experienced developer becoming demotivated.

## Why It Works
Modern software delivery has shown us that shorter feedback cycles, frequent communication and regular displays of progress are techniques valuable to any organisation. They help to minimise the risk of a project failing, and they are all inherent in good pair programming.

#### Programming Is Hard
We should all know that the most time consuming aspect of software engineering isn't typing, it's the time spent thinking about how to solve the current problem and to design a solution that works well. There are a huge number of choices that need to be considered with every line of code a developer writes, and pair programming helps share that responsibilty.

#### Increase Brainpower
Two heads are better than one and, in a pair, both developers will have knowledge in areas the other doesn't, meaning their ability to find good solutions is much better than it would be were they working alone. Additionally, because each idea a developer has needs to meet the approval of their partner, they're forced think a lot more critically about solutions, ultimately leading to better code.

#### Validation Of Ideas
Pairing encourages you to explain your thought process as you go, whether you're the driver or the navigator, and in a lot of cases there are several ways to solve a particular problem. By having a partner there to constantly bounce ideas off, you can quickly weed out sub optimal ideas and concentrate on the best solution.

## Benefits Of Pairing
There are many business benefits to pair programming, such as improving the quality of software delivered, building collaboration within a team and helping to share domain knowledge across multiple people.

#### Productivity & Focus
Working so closely with someone else means you've got no other option but to double down on the thing you're working on. The quality of the code becomes a shared responsibility, and means that, when pairing is done properly, it's much more difficult to become distracted by checking your emails, chatting to colleagues or browsing the web.

The back and forth nature of pair programming also helps to keep you engaged; whether you're switching roles every fifteen minutes, or you've gone the Ping Pong route, navigators are often eager to get back on the keyboard and keep momentum going.

#### Higher Quality
A developer working alone can often be tempted to take shortcuts, either in the interest of time or because they're not quite sure what the best solution is and don't want to feel stuck. It's much more difficult to let that happen when you're working as a pair, because everything you do is being evaluated by another person and you're both responsible for the quality of the code.

#### Domain Understanding
Pairing is a great way to share domain knowledge within an organisation, and makes it much easier for developers to move back and forth across different projects. By working this way, it means that if a particular developer is absent for any reason, whether it be holiday, sickness or they've decided to leave, there's at least one other person in the team who has a good understanding of the project and can easily continue working on it.

#### Improved Resiliency
Whatever environment you're working in, the number of things that can interrupt or distract a developer working alone is huge. When you're part of a pair, you become much more resilient to those interruptions because you're both committed to the task at hand. You're less likely to be interrupted by colleagues because they can clearly see that you and your partner are in flow, and you'll more easily resist the temptation to check emails because you're both committed to completing the task at hand.

#### Team Building & Cohesion
The stereoptypical view of software developers is that they work alone and are poor at communicating with others. Whether or not this sterotype is true, it's not uncommon to find developers who favour working alone and for teams, this is not ideal.

Pair programming encourages a much more social and collaborative way of working, which helps to build rapport between team members and a culture where your team solves problems collectively.

#### Learning
The number of technologies and languages within the field of software engineering is vast, so it's inevitable that there'll be areas where one developer is stronger than another. With pair programming, it becomes much easier for developers to learn from one another as they're being introduced to new concepts as they go.

#### Continuous Code Review
Code reviews are a valuable part of any organisation's software development lifecycle. Pair programming takes that concept to an extreme, by having the navigator constantly reviewing what the driver is typing, suggesting improvements or alternate approaches that might help catch edge cases.

## Challenges In Pairing
Moving from programming alone to becoming a strong pair programmer is not always an easy transition. We've encountered a number of specific challenges which you should watch out for.

#### Switching Mindsets
Programming has historically been a solo activity, so the mindset shift required to work on code together is significant. Developers often struggle to take onboard others ideas and externalise thought processes. This can be particularly challenging if you've worked solo for a long time and are not acustomed to social coding and working closely with others.

#### People & Time
As a business, you shouldn't expect two developers to complete a task in half the time. Often it will take a little longer than if a developer was working alone, so there is a short term cost associated with adopting pair programming. This additional cost is offset by the long term benefits of having higher code quality, less technical debt, and shared domain knowledge.

#### Exhaustion
Pairing is exhausting. When you've spent the entire day thinking critically about every line of code, justifying and communicating those thoughts and decisions, it's likely that you'll feel drained, but that you've achieved a lot. It's critical that you take regular breaks, that you have some flexibility, and choose appropriate times to pair.

#### Skill Disparity
You'll often find pairing works less well when you've got signifiant skill disparity between a pair. If one engineer is clearly more experienced and is making all the decisions, then this can lead to the less experienced feeling overwhelmed and demotivated, whch can lead to disengagement.

#### Pairing the wrong people
It's important that you pair developers who will be well suited to each other. The most beneficial pairing will be two people who can learn from one another, share similar philosophies and balance each other out. You don't want a pair of people known for over engineering solutions, or a pair with similar bad habits.

#### Backseat Driving
You don't want a situation where the navigator is literally dictating what the driver types #### this is an indication of skill disparity.

#### Communication (Your Baby Is Ugly)
Pairs need to be able to communicate openly and honestly with each other, if one has an idea that the other knows to be bad, they must be capable of saying so.

#### Disengagement
Some developers will be resistant to pairing or will spend their time less engaged in the activity. Developers checking their phone constantly, sitting back in their chair or not communicating actively are signs of an individual that is disengaged.

This is detrimental to the team, and it's important to try to understand why it's happening. It may be that the developer really does work better alone, or it's a sign that they're exhausted, there's disparity in skill between them and their partner, or that they simply don't get on with their partner.

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
