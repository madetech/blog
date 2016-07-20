# Code fragmentation: The modern day goto

## Programs are meant to be read by humans and only incidentally for computers to execute

Keeping your code simple and easy to change is one of the hardest challenges when writing programs.
One obvious aspect of this is the amount of code that you have to parse to understand what it aims to achieve.

All code can be divided into two categories.

- **Boilerplate:** Code that helps you, the developer.  It facilitates things like information hiding, type checking and encapsulation.
- **Domain:** The actual useful part of the program that is visible from the outside.

More fragmentation means that you are going to have more boilerplate to support it.

### Code Fragmentation

I primarily work with object oriented languages and I am always pleasantly surprised when I can achieve the same result in a fraction of the code by
using a functional language.  It just has a smaller surface area, is more compact and generally more expressive due to the underlying philosophies about how to model a domain.

Object oriented programs break up the data into small chunks and these are accompanied by the code that operate on them.
Most functional programming languages put the data first and have lightweight functions operate on it to create new representations.
This often has the nice side effect of the code being in a more central location.  The code is closer to the data.

If you practice object oriented programming correctly you are going to inherit a lot of fragmentation by default.
On top of this you can make it worse by prematurely optimising your code to accommodate potential new features.
Some people just write fancy code because their language makes it easy for them to do so.
What people forget is that a code is much easier to understand when you are writing it than when you read back over it, so they have no worries
writing complex code.  Mix in a bit of meta programming and you are dealing with an absolute disaster situation.

Code mixed in via modules, engines and gems to name but a few are some of the biggest painpoints that I have discovered in my day to day work.
Unneeded indirection is a classic form of incidental complexity.

It only means that you are going to have 20 files open in your editor to try and solve one problem.
Even the most advanced IDE cannot save you from this.
Your cognitive overhead has increased from understanding the code to mapping the code to where it is located.

### YAGNI and premature optimisation

A lot of the fragmentation comes when you prematurely optimise your system to be flexible and cater for edge cases that just never seem to occur.
Prematurely optimising for performance is another form of incidental complexity but not what I am referring to here.

Don't move the code to a different location unless you have established a clear boundary or separation of concerns that makes sense.
Do not extract code simply because you think that the class is too large.  If you can identify and extract a role from the class that is cohesive
then, and only then it is a good idea.

Be kind to your fellow developers.  Don't make them go on the hunt every time they want to write some code.
