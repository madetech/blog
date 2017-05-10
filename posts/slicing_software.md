# Slicing code

The primary goal of slicing software is to make it cheap to ship, and inexpensive to ship additional features.

A poorly thought out slicing strategy leads to viscosity. More advanced teams notice this typically the greatest around their test suites. On the whole, if you find test suites are slowing down the introduction of additional functionality and the evolution of your domain model, it is a sign that the coupling between your test assertions and the production code are less than ideal.

From this point on the following terminology is used:
- Refactor: the act of modifying the structure of the code, through a series of simple steps, while keeping all the tests passing.
- Rework: the act of rewriting sections of code, possibly guided by test suites, but potentially not in simple steps
- Transformation: the act of modifying code (production or test) for the purpose of changing its behaviour

In the worst cases, such as in the absence of automated test suites, teams feel the joint pain in wrong code slicing greatest. In situations without test suites, it can be much harder to realign slices to suit the needs of the team better - this is rigidity.

In situations with test suites, it may be necessary to undertake significant rework of those test suites to eliminate areas of rigidity. The danger with rework is that it has a significant risk of introducing behavioural defects. In the ideal case, simple paths are always present to allow refactoring, which has a lower risk of introducing behavioural defects.

One of the most valuable lessons from DDD (Domain-Driven-Design) is that no "model" is perfect, but some models are more useful than others. I use the terminology "model" to refer to how objects, or functions in the case of functional programming, collaborate to model the real world within the programming language chosen.

One of the reasons micro-services are incredibly useful is that they allow the models within each service to be radically different. Microservices are independently deployable, independently developable products within a sphere of a larger whole. Each microservice collaborates with other services, micro-services, and potentially third parties to fulfil a role. It is very rare for a micro-service to be isolated from other aspects of an ecosystem entirely.

Microservice architecture is an example of an extreme slice between two or more areas of code. Of course, slicing code in this way comes with benefits and (expensive) drawbacks. Technical teams should not make the decision to rework their systems into micro-services without being acutely aware of the disadvantages.

When beginning to build a system from scratch, the "domain model" is usually hard to determine up front. This "hard to determine all details up front" problem is especially the case if the intended approach is to build several different features over the course of multiple iterations. During those iterations, it may be necessary to go back and refactor/transform other features to be aware of new data within the domain model.

## AntiPattern: No Class has responsibility for the User 

One common slicing problem is related to domain objects themselves. Typically, these can be ORM classes or, they could be plain old objects with some behaviours.

One simple approach is to embed actions related to user stories into these domain classes, with UI classes also taking responsibility for some of this behaviour as well.

This design, seen commonly in the Rails-way, can work quite well for simple user stories; however, when the user stories become more advanced it can become harder to model the domain using a single ORM object, which means other ORM classes must also become aware of this action.

One property of well-designed tests is that they provide a living, up-to-date documentation of the system.

Agile is customer-focussed. However, this approach to not design around the customer causes the system design to not focus on the customer. To illustrate, consider unit test suites for each of these classes; they will each have knowledge of the user story.

Another way to describe this problem is with cohesion: a system exhibits low cohesion if that system forces multiple unit tests and different aspects of the codebase to be aware of the same user story. While fully minimising this lack of cohesion this is unlikely; it is important to keep an eye on cohesion and to increase it wherever feasible.

Focusing unit tests around user stories results in those unit tests describing customer expectations, rather than the expectations of another class operating in consort.

## AntiPattern: Black and White Mockist vs. Classical testing.

One common misconception is that "unit" refers to "a single class", but this leads to lots of fragmented test suites, and lots of usage test doubles. A strong coupling exists between test doubles and their production counterparts, and so can become a maintenance overhead. Every time a production counterpart changes, the test double must also be updated.

When multiple test suites must be understood to understand a user story, we see a fragmentation of knowledge. Every piece of fragmentation makes the code much harder to navigate and understand.

Unfortunately, the problem does not end here: when test suites are involved in too big a slice of the pie - in the extreme case of testing via the user interface, we see slow, brittle and incomplete test suites. Typically with this approach, it is also impossible to write the assertions that are needed to create complete coverage of behaviour.

Classical testing favours testing large swathes of the codebase, and cause test suites to have large fan-outs.

Mockist testing favours testing small amounts of code and using test doubles to reduce test-suite fan-out.

The answer is just enough classical testing, and just enough mockist testing to keep things flexible in the right places.

For example, a comprehensive test suite for the code that "Creates an Order" does not also need to exercise the database, but it does probably need to exercise some other objects hidden from it behind a public API.

So, it provides some test doubles for the database aspect. However, the details of any objects not cared about by the test suites can be hidden by the system under test. By doing so, we create a highly customer-focussed test suite with all the intricacies related to the user story for "Creating an Order", without also needing to provide test cases for the database. Before we saw test doubles become a maintenance overhead, but when cohesion is high we see the test double serving as an example for how the real database aspect should work.

By hiding what we want to be flexible (the model of creating an order) using classical testing, we can refactor the code related to "Creating an order" without changing the test suite or its assertions. We have created flexible code and a test suite that is largely agnostic to / protected from structural changes.


