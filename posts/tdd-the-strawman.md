# The Strawman: TDD

There have been a few rumblings recently between the subculture of TDD-lovers and the rest of the programming community, as always. I’ve heard reports that TDD doesn’t work, that it is snake oil, and that there are studies to suggest that TLD and TDD are no better than each other in a scientific study.

So, let’s dig a little deeper.

# "TDD doesn’t work because you end up with more complicated solutions because you need to mock."

I’m going to use the phrase “Test Double” to refer to the concept of a stand in for the purpose of testing, as for me a mock is a “true mock”, which is only one type of test double.

Test doubles are an interesting one for me - sure, there are times you need to use test doubles. I also will say using test doubles is bad. So, if I say that you should use test doubles, but it’s also bad then am I just making this up? Am I another one of those useless “TDD Consultants”?

To answer this question you’ve got to understand the single responsibility principle, and specifically when you cross into a clearly different family of behaviour. For example, your business logic can use a stand in database component. Having your code separated allows your business logic to own business rules and your database logic to own database rules.

# “You can’t use a stand-in database component as it won’t work like the real thing!”

Sure, it may not, but then I’d say this is a smell of something else. Those database components should construct entities (Domain objects in DDD lingo). The interface that these objects provide should not expose the underlying database. More often than not, they know nothing at all about the database. Sure, the database component can construct and receive them as a message, but that’s not the same as being ActiveRecord.

What does this mean? It means your database tables and schema can be entirely different to the entities that you use to model the domain for your business logic. Decoupling each of these concerns from each other allows you to evolve them independently.

Oh, and on the topic, that test doubles may not act like their real counterparts… Since the test double exists to allow you to check the behaviour of the code that uses the test double. If you made a test double that doesn’t match the production version, did you understand the production version fully? 

At this point it's probably worth mentioning that I rely on acceptance tests to as an integration suite to test against the real database, this happens without the UI. So here you should notice meaningful differences between production and your test doubles.

Here lies the reason why you should limit the number of test doubles: they are a pain to manage. So only use them when crossing a boundary into a new concern that should be decoupled. This could be into a new family e.g. business logic is decoupled from database code, or into a new bounded context e.g. a use case for the payments area of the system should be decoupled from the user accounts area of the system.

Another way to state this is that tests should exist to test for a single responsibility. As we know, responsibilities are reasons to change. Who requests changes? Hats (also known as actors). For example, in a financial system, there may be the following actors exerting influence on the software: accountants, tax authority, operations, sales, customers, to name just a few. If you want a modular, flexible system, it is important to separate tests (and indeed business logic) along these responsibility boundaries.

I’ve seen systems with lots of unit tests and indeed feature tests, but with the boundaries and responsibilities willy-nilly scattered all over the place. These systems become complicated and hard to change very quickly.

# “TDD doesn’t work when we try to solve problem X so we can’t use it for problems A, B or C”

I’ve heard that TDD cannot be used to write certain types of algorithms because you will end up with a brute force solution.  I think TDDing into a brute force solution is a very real end game of TDD.

Let's play this out. You have a brute force solution, a pretty decent test suite and probably quite a nice API around the code.  Brute force can sometimes be enough: optimise last. There are tonnes of brute force algorithms that I’ve written that are running in production. Why? They’re fast enough. So I’m not going to spend effort making the production code unnecessarily complicated to make it faster for no good reason.

In the cases where optimisation is necessary, you should be able to refactor the algorithm with the test suite acting as a safety net to verify you still have working code. You should be able to do this without touching your test suite. 

As a sidebar, though, under-performing algorithms can usually be avoided by being disciplined enough to apply the Transformation Priority Premise (TPP). Which, for example, when TDDing a sorting algorithm, means the difference between ending up in a bubble sort vs. a quick sort.
