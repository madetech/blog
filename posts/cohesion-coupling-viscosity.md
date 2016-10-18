# Cohesion, coupling and viscosity

One of the most important goals of a software engineer is to craft highly cohesive code. Cohesion refers to the grouping of code in a software system. 

Code is highly cohesive when the code contained within functions, methods, classes, or modules have much in common. Conversely, low cohesion occurs when elements of the code do not belong together and currently are. 

A code-base is said to be viscous when it is quicker to add a hack than to preserve the existing design.  To qualify this statement, evolving an Application's architecture, through a series of small refactorings, while keeping tests passing, is a form of design preserving activity. 

Another problem to contend with is unnecessary fragmentation of the code-base. Fragmentation does not result in viscosity specifically, but it can make it hard to build a mental map of the Application, especially in languages that do not have static types.

Fragmentation leads to friction; which is a feeling of lack of productivity that programmers get from a code-base as they attempt to make changes to it. Fragmentation is one of many sources of friction; others include lack of knowledge or experience in a particular paradigm. 

Systems can be highly cohesive when they are loosely-coupled, but it is a simplistic assumption to assume that loosely coupling everything has desirable outcomes. 

Extreme Programming (XP) practitioners are aware of the practice of Simple Design; amongst other things, minimising the number of moving parts is highly critical when building a software solution. 

An outcome of having high cohesion and appropriate loose coupling is that it reduces class/method/file/library churn. Remember! Code-churn introduces defects. Ergo, reducing code-churn reduces the introduction of defects.

# Tight coupling can be good

To discover why it is not always beneficial for areas of a system to be loosely coupled, we first must examine the "gold plated" architecture. Not everything needs to be dependency injected or mocked! 

A consideration of using test doubles is that it creates a test setup overhead. Due to this increased complexity, avoiding mocking is good unless we need to take advantage of class composition.

When we do not care about loose coupling is usually when a class provides very generic functionality or very specific functionality. 

A good example of generic functionality is the Array standard library. We can refer to this library as being very Adult, as it has many dependants. As such, it needs to be very stable and unlikely to change. To be tightly coupled to it is okay for this reason.

Tightly coupling to specific functionality, is useful when a class provides useful behaviour in a very specific domain. 

When a dependency's purpose is for specific functionality, and we are considering whether to tightly couple to it, care should be taken to ensure that the dependency has few dependents (it is Child-like). An ideal number is one or two dependents, but this is not a hard rule. 

Depending on an unstable class in only a small surface area of the code-base, allows the impact of changing it to be small.

# When tight coupling is bad

Exposing unstable dependencies illustrate the problem with tight coupling. Passing instability along a chain of dependencies spreads instability throughout application code, resulting in more viscous code.  

The strongest form of decoupling exists when communication occurs using simple data structures only. When an area of the system communicates using simple data structures only, I call this a boundary.

In object-oriented languages like Java, it is possible to use objects as data structures so long as they do not house any behaviour. Typically I tend to use objects with public fields in Java, data classes in Kotlin, and hash maps in non-statically typed languages.

Lack of boundaries, to ensure loose coupling, creates codebases with low cohesion and high viscosity, termed ball-of-mud codebases that are hard to change.

In the real world, it is common for business rules to depend on unstable child-like dependencies. This easiest way to ensure that the User Interface (UI) does not become coupled to these unstable dependencies is to have a boundary between the Business Logic and the UI.

Another angle to look at this problem is that the UI tends to evolve at a different rate to the business rules. For most Applications, although not all, the UI is more likely to change, which is understandable, as this is the most visible part of an Application and can be influenced by fashions. Business rules tend to change less frequently, and in fact, many core business rules can be reused across many different end-users if the abstraction is both loosely coupled and highly cohesive.

Regardless whether the UI or the Business Logic is changing more frequently, having them decoupled is beneficial to the continuous delivery of working software. An example used by Robert C. Martin is that it allows the business to see the cost of changes for each component individually, rather than as a summed figure. For example, if a client has requested functionality that causes the cost of the UI to be 10x more than the Business Rules, it may question why exactly that is. Would it be better to deliver a cheaper UI now?

To bring us back to approaches for decoupled software: one of the most powerful object-oriented techniques is class composition. It is also one of the most convenient, and easiest to understand, ways to achieve decoupling of behaviours.

It is wise to use class composition to invert your dependencies around areas which have different reasons to change. As an aside, employing dependency inversion allows the use of test doubles, which keeps architectural options open with regards to things such as the database, caching and authentication. 

For reasons described above, it is desirable to decouple your business rules from your database and use class composition around this dependency, so that it is possible to:

-  build a contract that we can create a test double for, which allows the business rules to be tested without the presence of the database, resulting in a fast test suite,
-  to allow the business rules to control the database in highly complex ways, and,
-  to ensure we can defer decisions about how we are going to deal with things like databases, schemas and ORMs

Database data structures are a very unstable aspect of a software application and are very likely to change. As such, it is bad for cohesion when your UI knows about the database or your ORM. Furthermore, it is bad for continuous delivery when you must change features that also depend on those ActiveRecord objects. Features themselves should be decoupled from the saving and retrieving of Business Objects.

The "database" interface expected by the Business Rules should return business objects. It is perfectly fine for these Business Objects to house some shared behaviour. These objects should not be ActiveRecord objects, as this would tightly couple the business rules with the highly unstable and very likely to change database structures. 

To add to the problems of being tightly coupled to the database is that it may force either:
- the representation of data in the database to be unoptimised for the storage engine
- the business rules to be aware of business objects that it should not care about
- naming conventions to be unclear

One common theme I see is paralysis during the software development cycle. Instead of worrying about the behaviour of the software, programmers expend enormous effort attempting to think ahead about what tables, columns, indexes and relations should exist before a line of business logic even exists. It is a much more natural and frictionless process to build business logic first, and then figure out how to store and retrieve these Business Objects later. 

Let's be clear. You have tight coupling and a viscous code-base when:

- Views call methods on ActiveRecord models
- ActiveRecord directly handles your HTTP post requests
- Rails controllers call methods on ActiveRecord objects
- Use case classes call ActiveRecord methods 

# Fragmentation

A good way to detect fragmentation is when related functionality is scattered across many classes, or even multiple libraries. 

The resulting pain point is that changing the structure of a system requires a mental map of multiple files, with a structure that does not reveal it is intent easily. 

Fragmentation can feel like viscosity, but it is a different problem entirely. In my experience, it is the most common result of gold plated architectures, which is a result of not adhering to Simple Design.

# SOLID

The reason that the Single Responsibility, Dependency Inversion and the Interface Segregation Principles exist is to solidify this point about coupling and cohesion. If a class has one reason to change, then it is highly cohesive. If the dependencies are inverted, and the interfaces are segregated, then it is exhibiting some forms of loose coupling.

I do not believe ignoring these very well-explored topics in the field of software programming, in the attempt to speed up delivery, is acceptable. The main mantra here is maintainability, both short and long term. 

Maintainability is the primary cost of software over its lifetime (unless its only purpose is to be deleted). Ergo, the primary value of software is its ability to tolerate and facilitate ongoing change. Customers want changes to their software to be cheap, and it is surprising how quick viscous code can accumulate and begin eating into the budget. Contrary to popular belief, it is only the secondary value of software that it meets its users' current needs.

As mentioned above when referring to XP's practice of Simple Design, high cohesion and loose decoupling is not synonymous with architecture gold plating or somehow unnecessary. It is the basic requirement for highly maintainable software. 

Another way to separate these concepts is to think of two classes of code defect; behavioural and structural. Most programmers, when referring to code defects, think solely of behavioural defects (i.e. the code does not function correctly). Structural defects are defects that affect maintainability. Structural defects are worse, as they affect the ability to add features, fix behavioural defects and therefore arguably have a higher cost over the life-cycle of a code-base.

I also do not accept that once well versed in building decoupled software, practising these techniques slows down delivery of software in the short-term. In fact, in the words of Robert C. Martin, "the only way to go fast, is to go well."
