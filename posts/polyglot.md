# Polyglot disciplines

## Problems

One of the biggest problems with switching between programming languages is the context switching. Remembering what operator is used to perform a particular language essential function e.g. `;` and `.` for statement termination or `.` or `->` for object member access.

The paradigm shift doesn't end with essential operators. A successful polyglot must also have an awareness of some basic tooling within each ecosystem. For example, a test framework, a web framework, how to represent time, how to represent currencies, concurrency gotchas. 

### Syntax

Differences in syntax are the first hurdle.

As an example, some languages favour parenthesis for function calls, some require them only in certain contexts, and others have special operators that allow you to completely avoid parenthesis, and others have no support for parenthesis at all!

These differences in syntax can be hard on the eyes and cause deterioration in mental focus, especially when the language is extremely unfamiliar.  

### Standard library

All languages come with a standard library, and very rarely are these even remotely similar from one language to another.

Every application needs to make some use of standard library operations. As examples: How do you concatenate strings? How do you open a file? What is the best way to create a JSON string?

Learning your way around these basic operations is the second thing I find myself learning after picking up the basic syntax.

### Paradigm

Ruby, Java, Python and C# share more in common with each other than they do with Erlang, Elixir, Haskell and Prolog.

There are languages which straddle these paradigm borders for example: OCaml and ECMAScript.

It's important to be well versed in the reasons these languages are different and embrace their strengths, and avoid their weaknesses. In a language which predominantly favours writing in an Object-Oriented style should be used as an Object-Oriented language, rather than attempting to go against the grain and using potentially more esoteric language features. 

Remember; as a polyglot your code should be understandable by a monoglot programmer who *only* knows the language you are currently working in.

### Culture

Every language, and every stack within a language, and every paradigm approach applied to a stack and language has a sub-culture and associated idiosyncrasies. 

As a polyglot it is more important to be idiomatic within a sub-culture, than it is to attempt to harmonise the various idiosyncrasies between the languages that you are personally familiar with. 

If you are working with a team on a project which has a particular culture and approach to their code, you should attempt to work within the style that the rest of the team are comfortable with. Only from this point is it wise to begin to influence changes, and gain support from the team to adopt those changes. 

Learning new cultures is by far the trickiest and requires a high degree of humility.

## My polyglot toolbox

Remembering all the differences between languages is hard work. Being a "specialist" in a language requires serious dedication, internalising knowledge about every corner of a language requires a lot of practical experience.

So how do I remember all of this? The secret is: **I don't**. 

Here, I'll tell you how I get by without being a specialist.

### Be familiar with the paradigms

It's important to learn new languages. The biggest piece of advice to those looking to become a polyglot is to pick languages that are vastly different to what you're working in now.

Working in Ruby? Pick a statically-typed OO language.
Know a statically typed OO language? Learn a functional language.
Know a functional language? Learn a logical programming language.
Know a logical programing language? Learn an old programming language.
Know an old programming language? Learn a new programming language.
Know a new language? Learn a systems programming language?
And so on.

The point here is comfortability - it is important to recognise that the difference between `C# and Java` (or `Ruby and Python`) is not significant enough to provide paradigm-changing learnings. Pick languages far outside your comfortable norm.

### Find a mentor

The importance of advice from someone who has worked with a language, in a team, has absolutely no comparison. There are tiny details of how "normal code" looks within a particular language that you can only pick up through osmosis and direct feedback from a mentor. 

I have found that meetups e.g. London Code Dojo, or London Software Craftsmanship are full of individuals who are able to provide mentoring over a kata. The subtle knowledge that can be transferred in less than 2 hours is substantial enough to be worth your time.

### TDD

The discipline with the biggest impact on my polyglot workflow is TDD. When I say TDD, I mean full on - properly Disciplined TDD, where **no line of production code** is written without first **writing a failing test**, and on top of that writing only the **simplest** thing to produce a failing test, and to produce a passing test. This means your assertions have to be watertight. There are a few situations where TDD isn't appropriate e.g. Testing CSS, Testing UIs, Testing FSM's, etc. (which I'll cover in another blog post). However, for the vast majority of code, IMHO, there is _zero excuse_ to not apply a rigorous disciplined TDD approach.  

The reason why TDD aids a Polyglot is that the feedback loop between an *assumption* (some theory about how a language feature works) is quickly backed up by a passing test or proven to be utterly false by a failing test. 

My life as a polyglot entails small, easy to digest, struggles with language features which I treat as tiny learning opportunities, and those learning opportunities keeps value flowing without getting "stuck". I have effectively replaced specialist knowledge in a particular language with a rigorous scientific approach to writing software. 

The flipside of this is that I don't need to remember how a language works, I can "re-learn" the finer details every single time I run my test suite, and I get a confirmation of my understanding _fast_.

### IDEs

IDE's are an underestimated source of learning opportunities. For example, IntelliJ gives realtime insights into better, equivalent ways of writing blocks of code in a range of different languages. My IDE also gives me hints on when I can simplify code in certain situations. Is `string.equals("a")` the simplest or is `string == "a"` going to work?

### Defer all technology decisions

### Separation of concerns

### Linters

