# When to avoid the DRY principle

The Don't Repeat Yourself principle is probably one of the most widely recognised
software design patterns out there. Most beginners in the industry will have heard
of it. More seasoned engineers will have taken it further and will see it's use in
other design patterns such as [Service-Oriented Architecture][1],
[Inversion of Control][2] and [Composability over inheritance][2].

It's easy to see why DRY is so well known as it's self explanatory, or at least it
is on the surface. To follow, don't repeat yourself. If you see a block of code that
looks similar or the same as a block of code in another file you'll likely think to
yourself, how can I abstract that?

DRY is all about abstraction. Abstraction is the use of interfaces such as functions
and classes to hide away implementation details. It's the method by which you keep
related bits of code together. Instead of writing 5 lines of code to print a web
page when a button is clicked, you may well place those 5 lines in a function called
`printPage()`. Abstraction is related to DRY in that when you place related pieces
of code together, they are easier to reuse and you end up repeating yourself less.
Therefore we can apply abstraction to DRY up our code.

Spotting and abstracting repetition isn't always obvious, it can get a little
nuanced at times. The more experienced engineer may spot less obvious repetition.
They might spot that in an e-commerce application there are multiple places where
products are selected from a collection based on some criteria and then some action
is performed on those products. They might choose to abstract the filter and map
operations on the collection of products into a reusable class. Someone less
experienced might not see this abstraction straight away.

## DRY might not always be the best idea

So we have this principle which is understood right from the start. You move
repetition into methods. It turns out a lot of code is repetitive. In some languages
you might use a for loop in nearly every file, should you abstract a loop? The
answer is: sometimes.

Like all things too much can be a bad thing. Sometimes the principle can be taken
too far, you can get too clever and end up with something that is harder to
understand or work with. I'd like to suggest a few situations where the principle
might not be so useful.

### Unnecessary abstraction

Repetitive code can often be abstracted unnecessarily. There are some very basic
examples of this. Take a capybara test that

### Too clever abstraction

### Wrong abstraction layer

[1]: https://en.wikipedia.org/wiki/Service-oriented_architecture
[2]: https://en.wikipedia.org/wiki/Inversion_of_control
[3]: https://en.wikipedia.org/wiki/Composition_over_inheritance
