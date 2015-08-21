# Comparing OOP and Component Based Design

In this article I'd like to discuss two concepts that you might not immediately
think to compare. I've written previously on keeping your
[stylesheets modular][stylesheet-modularity-post] and also on
[Object Oriented ideas][oop-post] so today I
bring the two loosely together.

Object Oriented Programming gives us the ability to organise our programs
or applications into objects. Objects represent real life things and also
computationally important things. They can represent a product, a cart that
holds products, the algorithm to find relevant products for a specific user, etc.

Object design draws the boundaries between the logic of our application and we
can then envisage the interaction of such logic. When designing with
objects we can visually imagine how they interact with each other. This broke
with previous ideas of proceedural program where we were forced to think of
programs as a continuous operation, one big list of commands to be executed.

Component based design teaches us to design UI in a modular way. Instead of
only designing pages and interfaces we instead build a library of independant
widgets that can then be pulled together to build pages and interfaces.

Very much in vogue at the moment, various conversations and solutions are
gaining popularity such as [Atomic design][atomic-design], [BEM][BEM],
[styleguide driven development][sdd], [Twitter's Bootstrap][twitter-bootstrap].

Styleguides are often used to pull together an applications components into a
navigatable list of examples. Mock ups can pull in these components to show
to clients. When it comes to implementation these components already designed
and accepted can then be used to build the end product.

Component libraries are a resource and product in themselves to clients. By
producing a library of components clients can later chose to build their own
pages reusing these resources. Such libraries are becoming a new currency in
client relationships for UI and UX. Instead of the old Photoshop .psd we're
selling the building blocks for unimagined structures.

Open source component libraries are popular too. The aforementioned Bootstrap
library by Twitter is perhaps the most predominant one.

[stylesheet-modularity-post]: https://www.madetech.com/news/rules-for-stylesheet-modularity
[oop-post]: google.com
[atomic-design]: http://bradfrost.com/blog/post/atomic-web-design/
[BEM]: http://getbem.com/introduction/
[sdd]: http://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/
[twitter-bootstrap]: http://getbootstrap.com/
