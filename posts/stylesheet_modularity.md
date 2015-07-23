# Rules for Stylesheet Modularity

Keeping applications organised takes a lot of work. Furious bursts of
development where deadlines are tight can lead to poorer design decisions. The
frontend in particular for me is harder to get right when the pressure is on.
I'm writing this post in order to clarify my hard and fast rules for writing
modular stylesheets in a rush.

My flavour of stylesheet modularity is in many ways a BEM implementation though
I'd certainly say I am no expert in BEM.

Without further ado, here are my rules:

 - One BEM module per file
 - Never reference one BEM Block from another
 - Never reference one BEM Element from another
 - Move repeating Element classes into their own Blocks
 - Keep your modules less than 100 lines long
 - Never name more than one class on an element
 - Do not style elements without classes
 - Compose rather than inherit

## One BEM module per file

### Example of doing it wrong

``` scss
.primary_navigation {}
.secondary_navigation {}
```

### Why

Easier to find modules if the filename matches the BEM Block class name.

### Notable exceptions

None.

## Never reference one BEM Block from another

### Example of doing it wrong

``` scss
.primary_navigation {
  .secondary_navigation {}
}

```

### Why

Easier to reason about where styles come from if all responsible styles are
defined in one file.

### Notable exceptions

None.

## Never reference one BEM Element from another Block or Element

### Example of doing it wrong

``` scss
.primary_navigation {
  .primary_navigation__link {}
}
```

``` scss
.primary_navigation__link {
  .primary_navigation__icon {}
}
```

### Why

Again it's easier to reason about styles when you do not nest style definitions
inside one another. It simplifies specificity problems.

### Notable exceptions

When Block is a modified block.

``` scss
.primary_navigation__link {}

.primary_navigation--mobile {
  .primary_navigation__link {}
}
```

## Move repeating Element classes into their own Blocks

### Example of doing it wrong

``` scss
.primary_navigation__link {}
.primary_navigation__link_icon {}
.primary_navigation__link_title {}
.primary_navigation__link_description {}
```

### Why

When you see commonly repeated words in Element classes this often is a sign
that you should break them out into their own module.

In the example of doing it wrong above, `.primary_navigation__link` could
become `.primary_navigation_link`.

``` scss
.primary_navigation_link {}
.primary_navigation_link__icon {}
.primary_navigation_link__title {}
.primary_navigation_link__description {}
```

### Notable exceptions

If it's one or two classes that are showing signs of being a new BEM Block I
might leave it until their are three.

## Keep your BEM modules less than 100 lines long

### Example of doing it wrong

I think you can understand this one without an example.

### Why

If you BEM module is getting lengthy then it's often a sign it's doing too much.
Breaking down large modules makes your code easier to reason about. It also
makes finding styles much easier!

### Notable exceptions

If it's just over 100 lines don't go crazy on yourself. If you're hitting
150-200 then you ought to start breaking your module down.

## Never name more than one class on an element

### Example of doing it wrong

``` html
<nav class="header_item primary_navigation">
</nav>
```

### Why

When you apply more than one class to an HTML element both those classes will
now be fighting for control over that HTML element. If you instead use two
different HTML elements you will save yourself a lot of headaches.

A corrected version:

``` html
<div class="header_item">
  <nav class="primary_navigation">
  </nav>
</div>
```

### Notable exceptions

One exception to this rule would be Modifier classes applied by JS. Imagine
you have an expanded version of your primary navigation,
`.primary_navigation--expanded` than gets enabled and disabled by JS. Instead of
removing the existing class you might instead just add the class to the element.
This is okay since a Modifier extends from the original class.

## Do not style elements without classes

### Example of doing it wrong

``` scss
.header {
  a {
    color: green;

    &:hover {
      color: blue;
    }
  }
}

.primary_navigation {
  a {
    color: red;
  }
}
```

### Why

Specificity is the problem yet again. If your BEM Block or Element finds itself
inside another BEM module and both style an element you will sometimes get
confusing results.

In the example above, when hovering over a link in `.primary_navigation` the
link would in fact go blue instead of staying red like you may expect.

Instead of styling HTML elements you should add a class to the said element
and style that, like so:

``` scss
.header__link {
  color: green;

  &:hover {
    color: blue;
  }
}

.primary_navigation__link {
  color: red;
}
```

### Notable exceptions

When styling WYSIWIG generated content that does not have any BEM classes it
is acceptable to style elements.

When I'm feeling lazy I do break this rule and it could perhaps be my most
broken rule.

## Compose rather than inherit

### Example of doing it wrong

``` scss
.primary_navigation {
  @extend %navigation;
}

.secondary_navigation {
  @extend %navigation;
}
```

``` scss
.primary_navigation {}

.secondary_navigation {
  @extend .primary_navigation;
}
```

### Why

Inheriting using `@extend` in SCSS couples your BEM modules too close together.
When this rule is broken alone it's not so much a problem. However if you break
my "Do not style elements without classes" or "Never reference one BEM Element
from another Block or Element" rule as well then you can get some funky results
especially if the class or placeholder you extended comes later in the alphabet
than the class extending it. I'll leave the rest of this why to the reader at
home.

### Notable exceptions

None.

## Summary

So there you have 'em. Learn these rules and practice them regularly and when
the heat turns up at work you'll hopefully not have a big ball of styles to
contend with a week or two later.
