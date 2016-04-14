# When to avoid the DRY principle

The Don't Repeat Yourself principle is probably one of the most widely recognised
software design patterns out there. Most beginners in the industry will have heard
of it. More seasoned engineers will have taken it further and will recognise it's
use in other design patterns such as [Service-Oriented Architecture][1],
[Inversion of Control][2] and [Composability over inheritance][2].

It's easy to see why DRY is so recognised as it's self explanatory, on the surface
at least. To follow simply don't repeat yourself. If you see a block of code that
looks similar or the same as a block of code in another file you'll likely think
to yourself, how can I abstract that?

DRY is all about abstraction, using interfaces such as functions and classes to
hide away implementation details. Moving 5 lines of code into a function that
has a name which summaries the 5 lines of code that will be executed when you 
call it.

Abstraction can be a little more nuanced too. The more experienced engineer will
spot less obvious repetition. They might spot that in an e-commerce application
there are multiple places where products are selected from a collection based on
some criteria and then some action is performed on those products. They might
choose to abstract the filter and map operations on the collection of products
into a reusable class.

## DRY might not always be the best idea

Like all things too much can be a bad thing. Sometimes the principle can be
taken too far, you can get too clever and end up with something that is harder
to understand or work with. I'd like to suggest a few situations where the
principle might not be so useful.

### Unnecessary abstraction

Repetative code can often be abstracted unnecessarily. There are some very basic
examples of this. Take a capybara test that

### Too clever abstraction

### Wrong abstraction layer

[1]: https://en.wikipedia.org/wiki/Service-oriented_architecture
[2]: https://en.wikipedia.org/wiki/Inversion_of_control
[3]: https://en.wikipedia.org/wiki/Composition_over_inheritance
