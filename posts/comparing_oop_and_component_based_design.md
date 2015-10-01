# Comparing OOP and Component Based Design

In this article I'd like to discuss two concepts that you might not immediately
think to compare. I've written previously on keeping your
[stylesheets modular][stylesheet-modularity-post] and also on
[boundaries in object oriented design][oop-post] so today I bring the two
loosely together.

Object Oriented Programming provides the ability to organise our programs
or applications into objects. Objects represent real life things and also
computationally important things. They can represent a product, a cart that
holds products or the algorithm to find relevant products for a specific user.

Object design is the drawing of boundaries between the logic of our
application and we can then envisage the interaction of such logic. When
designing with objects we can visually imagine how they interact with each
other. This broke with previous ideas of proceedural programming where we were
forced to think of programs as a continuous operation or rather, one big list of
commands to be executed.

If we wanted to devise yet another address book application we need to
encapsulate the ideas of an address book in code. We need to think about what
real world objects do physical address books have?

<img src="https://photos-2.dropbox.com/t/2/AABJ9YFWcNbhd38wD9LFT2bwM16QbPbkT48UoUbW8yaZhQ/12/8165609/png/32x32/1/1443708000/0/2/address_book_topology.png/COmx8gMgASACIAMgBiAHKAEoAg/K4oBg_ho_Sey5wDagTCqsdV7gV4eYIK9wHcGNIr6Kes?size=1280x960&size_mode=2" />

We first of all have the idea of an address book. The address book will then
have a number of entries. They have entries that may have one or
more addresses. Each address could be made of smaller objects such as an
address and phone number.

Splitting out our code into objects that represent real world "things" allow us
to discuss our code more easily. I can't imagine what it was like describing
a piece of procedural code.

> "Oh I think the if statement on line 45 for adding an item to the address book
> table is not quite working as expected"

versus

> "The 'add_entry' method of AddressBook isn't working as expected"

Abstraction is great for making things easier to understand whether you're
reading a class or discussing one with a colleague. Let us leave objects for
a moment...

We now find ourselves in the world of user interface design, if you're a backend
developer just imagine a wonderful world of vivid colors and shapes. More
usefully, component based design is a concept of modular UI design. It's a bit
like stepping from procedural to object oriented code.

To explore this concept we first must describe the age before. Typically when
building a new feature for a website a designer would provide us with a mock up
of the web page containing the feature. As a developer I would then begin to
build out that page within the app in my development environment to the design
provided. This change would then be deployed out to production.

Component based design changes this process though a designer may still provide
a mockup of the page with the feature. The difference is in implementation by
the developer. Instead of building the feature directly into the application
the UI of the feature would first be built into a style guide, sometimes known
as a pattern library.

The design would be broken down into individual elements. For example if a
feature required a table, the table would be added to the pattern library as
an individual module. Below is an example of Mailchimp's table from their
[pattern library](http://ux.mailchimp.com/patterns/tables).

![Screenshot from Mailchimp's pattern library](https://photos-5.dropbox.com/t/2/AAApkKwZl3nLRgK1Gs_CvKcuuPCd5dtaCZiPF7-Va0QoKg/12/8165609/png/32x32/1/1443535200/0/2/Screenshot%202015-09-29%2012.53.22.png/COmx8gMgASACIAMgBCAFIAYgBygBKAI/PYbVnE3v32CWUmFcbS24py8dtpZCKoY8bqJUFrxCSrI?size=1280x960&size_mode=2)

For each visual component in a feature the same process is applied until the
entire UI for the feature is documented as a set of modular components. Some
teams will then mock up the entire feature in a HTML page using something like
[pieces for rails](https://github.com/drpheltright/pieces). This is essentially
a HTML and CSS prototype that can be sent over to the designer to get their
take on the implementation. Once all parties are happy, the modules can be used
within the application to implement the feature.

Component based design is leaps and bounds ahead of the old page based design
since a byproduct is a reusable set of UI elements. The pattern library can be
reused in a number of ways to implement new features without necessarily
requiring an entire new design. Designers often had a file in photoshop or
illustrator without their UI widgets. The pattern library is essentially one
step closer to implementation in the app since they are made from HTML and CSS.

Very much in vogue at the moment, various conversations and solutions are
gaining popularity such as [Atomic design][atomic-design], [BEM][BEM],
[styleguide driven development][sdd], [Twitter's Bootstrap][twitter-bootstrap].

Component libraries are a resource and product in themselves to clients. By
producing a library of components clients can later chose to build their own
pages reusing these resources. Such libraries are becoming a new currency in
client relationships for UI and UX. Instead of the old Photoshop .psd we're
selling the building blocks for unimagined structures.

Open source component libraries are popular too. The aforementioned Bootstrap
library by Twitter is perhaps the most predominant one finding it's way into
all kinds of admin interfaces, CMS's, documentation and open source sites.

One of my own hopes is that in the future we can work even closer with designers
to build these libraries of components by iterating on mockups with HTML and
CSS. We'd get the first ever mockup from a designer, we'd implement this in
HTML and CSS, then extract out into the library and by the time the next feature
comes around the designer can consult the pattern library and produce mockups
using them. If the designer could maintain such a library within the application,
that would be a dream!

There are so many benefits from this way of working, there's a reason pattern
libraries / styleguides are getting more popular.

Being able to describe UI components by name will make conversations with
designers and developers much easier just like objects do for code. So too
will be pulling these components together into mockups that can be iterated on
without implementing any backend code at all.

Having reusable UI modules that can be mixed and matched mean we can reuse
components more regularly, we can save time! Again this is just like OOP.

We get the added benefit of our components being decoupled making the process
of updating them less risky since they won't be leaking into other areas of
the design. When we update a component we can simply interate within the
pattern library ensuring all the states of the component still look okay. It's
pretty much REPL driven development for UI!

I'm rather excited about all this :)

[stylesheet-modularity-post]: https://www.madetech.com/news/rules-for-stylesheet-modularity
[oop-post]: https://www.madetech.com/news/boundaries-in-object-oriented-design
[atomic-design]: http://bradfrost.com/blog/post/atomic-web-design/
[BEM]: http://getbem.com/introduction/
[sdd]: http://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/
[twitter-bootstrap]: http://getbootstrap.com/
