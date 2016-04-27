# We tried Clojure for a day and this is how it went
  - We use and love Ruby
  - So why Clojure?
  - Made Learning Day
  - The good
  - The bad
  - What's next?

## We use and love Ruby

Ruby really is my favourite programming language. I love the clean syntax and the freedom that it gives you.
Beyond debugging meta programming in gems far far away, I have no real problems with solving problems in it.
Many people say that it is too slow, but I have found that effective caching and background processing negates this for the majority of typical web
apps.

## So why Clojure?

We all know the awesomeness that makes Lisp unique:

  - [Homoiconic] (https://en.wikipedia.org/wiki/Homoiconicity)
  - [Function composition] (https://en.wikipedia.org/wiki/Function_composition)
  - [Macros] (https://en.wikipedia.org/wiki/Macro_(computer_science))
  - Advanced interactive development
  - Data first
  - Simplicity

One thing that got me interested in it was that there was some sort of natural progression in style of coding over the years.
I started placing more value in data and started seeing stateful and stateless code as a separation of concerns.
Lisp seemed to have all these principles baked into its core yet I had to work so hard to get them in procedural languages.

## Made Learning Day
  We recently had a day dedicated to learning / exploring something that may benefit to our daily work.
  Whether it be a programming language, library, service or whatever.
  This would be the perfect opportunity to share my interest in the language.

  We would be divided into 3 teams with one person at the head of each team to lead the way.
  We all pitched our ideas and got people to join if they were interested.

###The 3 winning suggestions were:
  - [Clojure](https://clojure.org/)
  - [Elixir](http://elixir-lang.org/)
  - [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language))

Leading team Clojure, I far from a professional but knew enough to get us started.

###Some of my previous lisp experience included:
- Configuring Emacs
- Smashing as much of the [Wizard book](https://mitpress.mit.edu/sicp/) into my brain as possible.
- [Clojure](http://www.braveclojure.com) for the Brave.
- Random katas.

My two team mates were Chris and Nick, and they were pretty enthusiastic about it.

[London Google Campus](https://www.campus.co/london/en) would be our location.

I did a quick introduction to Lisp including history, features like the reader, macros, data structures, and why I think this language was worth
researching.

Our approach wasn't going to be to zone in on any one aspect of the language.
Instead I opted for building something useful as quickly as possible.

###At the end of the day I hoped to achieve the following:
- A CRUD product system, backed by Mysql.
- Have at least one unit test.
- Make it presentable for demo.

### Stretch goals
- Caching
- I18n
- Image uploading
- Deployment to Heroku

We would use [Luminus](http://www.luminusweb.net/) (whoops nearly said framework there) for creating the program.
The documentation has an awesome example of building a xxx system, and we were going to adapt this to build our own product CRUD system.
So we started hacking away at it, picking random tickets that we had created in Trello.

###The good
- Having to reboot the JVM for changes to be picked up.
- Plain SQL, we missed our ORM's! (as imperative programmers do)
- Java stacktraces.  The volume of data made it feel like we were not escaping any complexity.
- Testing culture in general was different, and struggling to get into our red / green / refactor cycle.
- Less convention over configuration than we were used to. We had to actually think about glueing stuff together.

###The bad
- We were able to make significant progress in 5 hours and had a lovely "stable" website to demo.
- Fun talking about the origins of Lisp and realising how different it is from object oriented programming.
- Beautiful Maps without commas
- Variety of intesting datatypes.
- Preview to how awesome the community is. Because the barrier to entry is higher than Ruby I find that there are a lot more smart accademic types.
- The safety that immutable datastructures bring.  You have to be explicit about shooting yourself in the foot.
- Rainbow parentheses!

Nick wrote what I would consider the best function of the day.
  ```clojure
  (defn slug-from-name [name]
    (clojure.string/lower-case (clojure.string/replace name #"\s+" "-")))
  ```

##What next?
It is optimistic to assume that you will be sold on a language in 5 hours of experimenting with it.
To be honest I felt quite a bit of pain as I was trying to write Clojure in my default imperative way of thinking.

I will continue to study Clojure and bring it up again for a research topic at the next MLD!
