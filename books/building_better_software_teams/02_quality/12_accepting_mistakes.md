# Learning From Mistakes

As software engineers, we're faced with new problems and challenges every day. No matter how well we know a programming language, how many projects we've worked on throughout our careers or how much time we've spent creating repeatable solutions to common problems, there will always be something new that requires critical thought.

Inevitably, then, we will make mistakes. Deadlines will not always be met, solutions may not always be correct, and critical tasks may be overlooked. These are not Bad Things.

When we're walking an unfamiliar path, we're bound to make the occasional wrong turn. What's important is that we know that those mistakes have a lot to teach us, and that we're in an environment where it's safe to make those mistakes.

## Avoiding Blame

From an early age, we're encouraged to assign blame when something negative happens, if only to avoid negative consequences towards ourselves. This continues into adulthood and our careers, with the assumption being that your employees work as hard as they do to, in part, avoid making mistakes and then being blamed for them. The belief is that without negative consequences to failure, your employees will be less engaged and less motivated.

This attitude is counterproductive to a healthy working environment. Giving your team a space in which mistakes and failures can be accepted and learned from doesn't mean encouraging lower standards, but ensuring your team and your organisation as a whole can continue to evolve and grow.

It's also important to recognise that mistakes and failures are not necessarily the result of willfully deviant behaviour. Tolerating mistakes, and recognising that they are opportunities for everyone to learn rather than for one person to be blamed, is a skill.

## Understanding why mistakes happen

Within software engineering and delivery, there are many different reasons why mistakes or failures might happen:

### The task is unfamiliar to everyone involved

Mistakes will most often be made when attempting to solve a problem for the first time, and as software engineers, we're faced with a constant stream of fresh challenges. It's our job to design solutions that meet requirements, but we're not infallible. The solution may fail in unforeseen ways, or we may need to revisit the task and find that we've made more work for ourselves by creating something inefficient.

### Skill disparity

Similar to the previous example, less experienced members of the team may struggle with tasks other engineers find simple. Compounding the issue, those same team members might then feel the need to prove themselves by forging ahead and trying to figure out the problem on their own.

### Routine, but complex manual processes

Software engineers love to automate all the things, but there'll always be the occasional process that needs to be performed manually (or at least hasn't been automated yet) and, no matter how often the process is performed, the more convoluted it is, the more likely it is that a crucial step is overlooked, leading to a failure.

For example, consider a typical continuous delivery pipeline. Engineers craft their code locally, test the build, commit it to source control, and push it through the pipeline. If the engineer forgets to test the build and commits faulty code, which causes tests to fail during the build step of the pipeline, breaking the build, and preventing that code from moving further down the pipeline. The pipeline is then blocked until either the developer fixes their mistake, or a rollback to the last successful build occurs.

This is the purpose of the build step of the pipeline, but in an ideal world the engineer would have simply run those tests, discovered the error and fixed them locally.

### Poor understanding of requirements

In most software teams, strides are taken at the beginning of a cycle of work to gather as much data and information as possible from the client to understand requirements as completely as possible.





- mistakes a crucial part of learning, discovery and experimentation
  - for example, failure within routine operations could be a sign that the operation is too complex
  - “We’re in the discovery business, and the faster we fail, the faster we’ll succeed.”

- embracing failure does not mean encouraging people to be deviant
  - inattention could be deviant behaviour, but it could also be a sign that your employees are burnt out

- detecting mistakes

- analyzing mistakes
  - retrospectives

- promoting experimentation
