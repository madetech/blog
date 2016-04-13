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

The more experience engineer will spot less obvious repetition. They might spot
that in an online store, products selected from a collection based on some
criteria then some action will be performed on those products. They might choose
to abstract the filter and map operations on the collection of products into a
reusable class.

# DRY might not always be the best idea

Like all things too much can be less than favourable for you. Sometimes the
principle can be taken too far, you can get too clever and end up with something
that is harder to understand or work with. I'd like to suggest a few situations
where the principle might not be so useful.

[1]: https://en.wikipedia.org/wiki/Service-oriented_architecture
[2]: https://en.wikipedia.org/wiki/Inversion_of_control
[3]: https://en.wikipedia.org/wiki/Composition_over_inheritance
