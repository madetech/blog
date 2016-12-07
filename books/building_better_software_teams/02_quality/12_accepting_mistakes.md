# Learning From Mistakes

As software engineers, we're faced with new problems and challenges every day. No matter how well we know a programming language, how many projects we've worked on throughout our careers or how much time we've spent creating repeatable solutions to common problems, there will always be something new that requires critical thought.

Inevitably, then, we will make mistakes. Deadlines will not always be met, solutions may not always be correct, and critical tasks may be overlooked. These are not Bad Things.

When we're walking an unfamiliar path, we're bound to make the occasional wrong turn. What's important is that we know that those mistakes have a lot to teach us, and that we're in an environment where it's safe to make those mistakes.

## Avoiding Blame

From an early age, we're encouraged to assign blame when something negative happens, if only to avoid negative consequences towards ourselves. This continues into adulthood and our careers, with the assumption being that your employees work as hard as they do to, in part, avoid making mistakes and then being blamed for them. The belief is that without negative consequences to failure, your employees will be less engaged and less motivated.

This attitude is counterproductive to a healthy working environment. Giving your team a space in which mistakes and failures can be accepted and learned from doesn't mean encouraging lower standards, but ensuring your team and your organisation as a whole can continue to evolve and grow.

It's also important to recognise that mistakes and failures are not necessarily the result of willfully deviant behaviour. Tolerating mistakes, and recognising that they are opportunities for everyone to learn rather than for one person to be blamed, is a skill.

## Why mistakes happen

Within software engineering and delivery, there are many different reasons why mistakes or failures might happen, including:

### The task is unfamiliar to everyone involved

Mistakes will most often be made when attempting to solve a problem for the first time, and as software engineers, we're faced with a constant stream of fresh challenges. It's our job to design solutions that meet requirements, but we're not infallible. The solution may fail in unforeseen ways, or we may need to revisit the task and find that we've made more work for ourselves by creating something inefficient.

### Skill disparity

Similar to the previous example, less experienced members of the team may struggle with tasks other engineers find simple. Compounding the issue, those same team members might then feel the need to prove themselves by forging ahead and trying to figure out the problem on their own, rather than communicating with their peers.

### Routine, but complex manual processes

Software engineers love to automate all the things, but there'll always be the occasional process that needs to be performed manually (or at least hasn't been automated yet) and, no matter how often the process is performed, the more convoluted it is, the more likely it is that a crucial step is overlooked, leading to a failure.

For example, consider a typical continuous delivery pipeline. Engineers craft their code locally, test the build, commit it to source control, and push it through the pipeline. If the engineer forgets to test the build and commits faulty code, which causes tests to fail during the build step of the pipeline, breaking the build, and preventing that code from moving further down the pipeline. The pipeline is then blocked until either the developer fixes their mistake, or a rollback to the last successful build occurs.

This is the purpose of the build step of the pipeline, but in an ideal world the engineer would have simply run those tests, discovered the error and fixed them locally.

### Poor understanding of requirements

In most software teams, strides are taken at the beginning of a cycle of work to gather as much data and information as possible from the customer to understand requirements as completely as possible. Nevertheless, it's not unheard of for a seemingly unimportant detail to be overlooked during this phase of the project, only to either become a blocking problem midway through development, or to go completely unnoticed and later be revealed as a key requirement whilst you're showcasing your work.

### Research spikes that lead to nothing

In an effort to plug knowledge gaps, or trial untested solutions, research spikes are occasionally carried out. On a software team, this would typically involve one engineer dedicating a small but significant amount of time, such as half a day or a whole day, to investigating whether a potential solution is worth spending more time on. Said solution proving to be unsuited to the task at hand, and the cost of time spent investigating it, could be seen as an undesirable result.

### Team happiness

Happy engineers are productive engineers. When something is making an engineer unhappy they can lose focus, and the quality of their work can suffer as a result, occasionally leading to bigger problems.

## Why a mistake is A Good Thing

> We’re in the discovery business, and the faster we fail, the faster we’ll succeed.

> _Amy Edmondson_

The best way to deal with mistakes and failures is to treat them as opportunities to learn, both individually and as a team, after all, when we're embarking on a new challenge, making mistakes is a crucial part of the discovery and experimentation process.

In other situations, such as mistakes occurring within a complex routine process, you have the opportunity to reflect on what went wrong, why, and how you can simplify the process to either reduce or eliminate mistakes.

This mindset of actively discussing and learning from mistakes, rather than blaming anybody for them, doesn't mean you're encouraging your team to slack off and take shortcuts to the detriment of the project. Even in situations where a mistake can be attributed to an individual's lack of care or inattentiveness, there's the chance to dig deeper and discover what led to that behaviour, and what you can do to improve the situation for the individual and your team.

## Creating an environment in which it's safe to make mistakes

Your team needs to know that mistakes can be tolerated, and the best way to convey this is to have open discussions about problems that have arisen, without playing the blame game. Take the time to talk about why a mistake happened.

In the examples given earlier, we discussed reasearch spikes, time given to investigating whether a potential solution is worth pursuing or not.

- needs more

### Discovering Mistakes

Big mistakes are easy to spot. In software, you know something's gone wrong if, for example, a build fails, critical data is lost or a website goes offline. Steps are immediately taken to fix those mistakes and resume normal service. Smaller mistakes and failures are much more easily hidden, both passively and actively, and the earlier these are discovered, the better.

- needs more

### Understanding Mistakes

Once you've discovered the mistake, you need to find out what it can teach you and how it can help you in the future. One of our favourite tools for addressing mistakes and failures discovered within our work is the retrospective.

Retrospectives happen at the end of a sprint, usually every week or two, and give everyone a platform on which to highlight things that went well, and things that didn't go so well. Providing you've built an environment in which it's safe to be honest about shortcomings and mistakes, retrospectives are a great way to uncover process failures and to voice concerns about the work that may lead to avoidable mistakes.

An example we've encountered during a retrospective is realising that our mistake was not getting enough detail on requirements during the planning stage. This led to us moving down a path of work that we ultimately discovered was incorrect when we presented it to the customer. We then had a discussion as a team over how that had happened, and came away with a greater understanding of the sort of information we need to gather early in the process, as well as actionable steps we could take to reduce the risk of it happening again.

## Conclusion

...
