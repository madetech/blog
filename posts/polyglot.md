# Polyglot disciplines

As a polyglot software engineer, I have discovered some disciplines which I have found beneficial to me. My hope is that readers of this article will find the experience I share here profitable to their endeavours as polyglots (or indeed as monoglots). 

## Problems

One of the biggest problems with switching between programming languages is the context switching. Remembering what operator is used to perform a particular language essential function e.g. `;` and `.` for statement termination or `.` or `->` for object member access.

The paradigm shift doesn't end with essential operators. A successful polyglot must also have an awareness of some basic tooling within each ecosystem. For example, a test framework, a web framework, how to represent time, how to represent currencies, concurrency gotchas. 

### Syntax

Differences in syntax are the first hurdle.

As an example, some languages favour parentheses for function calls, some require them only in certain contexts, and others have special operators that allow you to avoid parentheses completely, and others have no support for parentheses at all!

These differences in syntax can be hard on the eyes and cause deterioration in mental focus, especially when the language is extremely unfamiliar.  

### Standard Library

All languages come with a standard library and very rarely are these even remotely similar from one language to another.

Every application needs to make some use of standard library operations. As examples: how do you concatenate strings? How do you open a file? What is the best way to create a JSON string?

Learning your way around these core operations is the second thing I find myself learning after picking up the necessary syntax.

### Paradigm

Ruby, Java, Python and C# share more in common with each other than they do with Erlang, Elixir, Haskell and Prolog.

There are languages which straddle these paradigm borders, for example, OCaml and ECMAScript.

It's important to be well versed in the reasons these languages are different and embrace their strengths, and avoid their weaknesses. A language which predominantly favours writing in an Object-Oriented style should be used as an Object-Oriented language, rather than attempting to go against the grain and using potentially more esoteric language features. 

Remember; as a polyglot, your code should be understandable by a monoglot programmer that *only* knows the language you are working in currently.

### Culture

Every language, every stack within a language, and every paradigm approach applied to a stack and language have a sub-culture and associated idiosyncrasies. 

As a polyglot, it is more important to be idiomatic within a sub-culture, than it is to attempt to harmonise the various quirks between the languages that you are familiar with personally. 

If you are working with a team on a project which has a particular culture and approach to their code, you should attempt to work within the style that the rest of the team finds comfortable. Only at this point is it wise to begin to influence changes and gain support from the team to adopt those changes. 

Learning new cultures is by far the trickiest and requires a high degree of humility.

## My polyglot toolbox

Remembering all the differences between languages is hard work. Being a "specialist" in a language requires serious dedication, internalising knowledge about every corner of a language requires a lot of practical experience.

So how do I remember all of this? The secret is: **I don't**. 

Here, I'll tell you how I get by without being a specialist.

### Familiarise yourself with new language paradigms

I have found it is important to learn new languages (but not just any new language, as I will cover). The biggest piece of advice to those looking to become a polyglot is to pick languages that are vastly different to what you currently find comfortable.

Working in Ruby? Choose a statically-typed OO language.

Know a statically typed OO language? Learn a functional language.

Know a functional language? Learn a logical programming language.

Know a logical programing language? Learn an old programming language.

Know an old programming language? Learn a new programming language.

Know a new language? Learn a systems programming language.
And so on.

The point here is comfortability - it is important to recognise that the difference between `C# and Java` (or `Ruby and Python`) is not significant enough to provide paradigm-changing learnings. Pick languages far outside your comfortable norm.

### Find a mentor

The importance of advice from someone who has worked with a language, in a team, has absolutely no comparison. There are tiny details of how "normal code" looks within a particular language that you can only pick up through osmosis and direct feedback from a mentor. 

I have found that meetups e.g. London Code Dojo or London Software Craftsmanship are full of individuals who can provide mentoring over a kata. The subtle flow of knowledge that takes place in less than 2 hours is substantial enough to be worth your time.

### TDD

The discipline with the biggest impact on my polyglot workflow is TDD. When I say TDD, I mean full on, disciplined TDD. 

TDD is a strict discipline where a programmer is not able to write a single line of production code without writing a failing test. Given the tests must be written, and written first, when TDD'ing a programmer is also only allowed to write the simplest assertion to produce a failing test. When a programmer has a failing test, they are also only allowed to write the simplest production code to make that test pass. What this yields in practice are watertight assertions in your test suite. 

As an aside; there are a few situations where TDD isn't appropriate e.g. testing CSS, testing UIs, testing FSM's, etc. (which I'll cover in another blog post). However, for the vast majority of code, IMHO, there are zero excuses not to apply a rigorous, disciplined TDD approach.  

The reason why TDD aids a Polyglot is that the feedback loop between an *assumption* (some theory about how a language feature works) is quickly backed up by a passing test or proven to be utterly false by a failing test. 

My life as a polyglot entails small, easy to digest struggles with language features which I treat as little learning opportunities, and those learning opportunities keep value flowing without getting "stuck". Through leveraging these feedback loops, I have replaced specialist knowledge in a particular language, with a rigorous scientific approach to writing software. 

The flipside of this is that I don't need to remember how a language works, I can "re-learn" the finer details every single time I run my test suite, and I get a confirmation of my understanding _fast_. On top of this, I can fake having an in-depth knowledge in a variety of tech stacks while under pressure of a customer engagement.

#### Cultural Paradox

TDD is a team skill. You do not get the full benefits of it unless your whole team is regularly practising it. As such, it is also a cultural thing, and some teams do not have the belief in it, or may not practice it in a disciplined way. As a polyglot, when a team does not practice TDD it puts more pressure on me to become increasingly specialised in a particular tech stack. My advice as a polyglot is to introduce TDD as early as possible to teams who lack this disciplined approach. 

### IDEs

IDE's are an underestimated source of learning opportunities. For example, IntelliJ gives real-time insights into better, equivalent ways of writing blocks of code in a range of different languages. My IDE also gives me hints on when I can simplify code in certain situations. Is `string.equals("a")` the simplest or is `string == "a"` going to work?

### Defer Technology Decisions

As an agilist one thing I want to be delivering is a continuous stream of value. One thing that I find to be of high friction is new technologies. 

The most common decision that I would suggest deferring is the answer to this one question: "What is the database schema?". Some Engineers will gasp at this point, but hold back any disbelief in this for a moment. When decisions like what the database schema is and when you architect your code to be truly agnostic of a particular web framework are deferred, something interesting happens, you can worry about what your customer needs without learning anything but a test framework and the language at hand. You can worry about learning how to solve those details later. Not only that, but you'll be more informed to make the right decision about the framework or the database as you'll have more knowledge about the shape of the solution. Maybe a lightweight database is enough (or even flat files!), or maybe Sinatra is sufficient to get the job done.

The amount of time I've spent in the past attempting to get to grips with Spring, Rails, or GraphQL or some fancy new impressive stack before I've even begun learning and feeding back with customers is argument enough for me to defer these decisions. It prevents me from becoming distracted with the mission to solve the customer's goal simply.  

In most business systems, Customers do not need to see a UI to provide feedback and for you to be generating useful learnings about their domain. Considering the flow of data to and from the UI through the behaviours of the system will produce a multitude of questions for your customer and domain experts. Obviously, a UI is inevitable, and not something you should hold off forever, but you can throw that on top as icing on the cake after the first iteration. 
