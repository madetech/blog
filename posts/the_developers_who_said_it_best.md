# The Developers Who Said It Best

## My favourite programming quotes


Those who forget the past are condemned to repeat it.

Writing code is an art form. There is no one correct way to do things, so we strive to solidify our understanding of what works and what doesn't.
This makes things interesting.  In my quest to understand how to write good programs, some quotes have resonated with me.

Below are some of my favorite ones, and pop up in my head ever so often when I am in doubt.

### *"For each desired change, make the change easy (warning: this may be hard), then make the easy change"*

**- Kent Beck**

Also known as [Preparatory Refactoring](http://martinfowler.com/articles/preparatory-refactoring-example.html), you sometimes need to take a step back
to gain agility in implementing your new feature.
Refactoring should be included as part of the feature, and should not be treated as a separate task in my opinion.
It may feel counter intuitive especially when there are tight deadlines, but this usually results in a more robust solution.

---

### *"Bad programmers worry about the code. Good programmers worry about data structures and their relationships."*

**- Linus Torvalds**

I find this quote so important that I have written an entire [blog post](https://www.madetech.com/blog/data-structures-at-the-heart-of-your-system) about this.  Smart data structures lead to dumb code which is always desirable.  You are pushing the decision making down into the primitives, and end up with a system that has suffers from less cyclomatic complexity.

---

### *"The trouble with programmers is that you can never tell what a programmer is doing until it’s too late."*

**- Seymour Cray**

A bit harsh but it is easy for even the most experienced developers to head down the wrong path when trying to solve a problem.
This is usually a result of poor communication. There needs to be constant discussions between the developer and the stakeholders or expectations can
go out of sync.

---

### *"Good design is obvious. Great design is transparent."*

**- Joe Sparano**

I feel like this is very much related to the [Principle of least astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment).
If making a change is boring because you only needed to navigate to where you expected the logic to be contained, you will not find it very interesting.
If however you have to absorb some of the obstacles that the previous author of the code wrote, it can be more challenging.

---

### *"Besides a mathematical inclination, a [..] mastery of one's native tongue is the most vital asset of a competent programmer."*

**- Dijkstra**

In order to express yourself well through code, you must master the language that you write / speak in.
Naming concepts in a program can make it understandable or a total mess. I often open a thesaurus to double check that the name that I have selected
is as expressive as it can be. Code should be written to be understood by humans first and computers second.

---

### *"Functions that create values are easier to combine in new ways than functions that directly perform side effects"*

**- Marijn Haverbeke**

Pure functions are easy to test and faster than functions with side effects.
I always try create as many pure functions as possible and have an imperative layer wrap these to do the interacting with the volatile outside world.
Haskell has taken this concept so far that it does not allow side effects apart from ones wrapped in the IO monad.

---

### *"The purpose of abstraction is not to be vague, but to create a new semantic level in which one can be absolutely precise"*

**- Edsger Dijkstra**

Definitely one of my favorite quotes of all time.  When you create a code seam, and name it correctly it can house a specific piece of knowledge and
can be thought about in isolation. Class and method extraction refactorings are some of the tools used to accomplish this.

---

### *"When in doubt, use brute force."*

**- Ken Thompson**

Quite often we encounter bugs that seem impossible to comprehend. You need to eliminate all the variables in order to get to the root
cause of the problem.
You need to cut through the layers of abstraction to get to the actual piece of buggy code. Strace, Tcpdump and Wireshark exist for when you have
exhausted all your options but hopefully will not come to that.

---

### *"A language that doesn’t affect the way you think about programming, is not worth knowing."*

**- Alan Perlis**

There are so many interesting programmnig languages that aim to solve problems in different ways.
Don't waste time learning new languages that follow the same paradigm but only differ in syntax, you probably understand the underlying concepts
anyway.

---

### *"All code in any code-base should look like a single person typed it, no matter how many people contributed."*

**- Rick Waldron**

It is very important to keep consistency throughout the codebase.
Event if you think a style of solving problems can be improved upon, stick to the existing way of doing so.
If you want to refactor it to be better, do so to all the code at the same time.

---

### *"Given enough eyeballs, all bugs are shallow."*

**- Eric S Raymond**

Here at Made we pair quite frequently on writing code.  It is incredible how much can go undetected if you are doing things on your own.
Pull requests is another excellent form of keeping code quality high.
