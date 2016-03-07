# Componentisation and the Single Responsibility Principle

Keeping a good separation of concerns means writing code that only handles as much as it needs to. It's a concept that should affect every piece of code you write, from class definitions to database tables. Only store the data which is relevant. Only encapsulate the logic which is covered by the responsibility of your class. My colleague wrote about this recently when discussing [Inheritance and Composition][luke_inheritance_composition].

Keeping a good separation of concerns has historically been tricky in front end code. Having to bind JavaScript classes to `window` for example, and use classes to link together JavaScript, HTML and CSS. These are loose ways to tie together disparate code. Ideally code should be tied directly to any relevant aspects.

It's gotten a lot easier with client side JavaScript, developers are reaping the benefits of small, open source modules more easily through package managers like [NPM][npm] and [Bower][bower], and writing modular, DRY code by employing module loading systems like [Browserify][browserify] and [AMD][amd]. As Single Page Apps get more popular, though, a lot of the weight of an application is shifting into JavaScript, and the rest of the application can feel cumbersome by comparison.

It has always been difficult, not to mention finicky, to keep HTML and CSS code modular. At Made we use best practices like [BEM (Block, Element, Modifier) rules][bem] to 'namespace' DOM elements, allowing us to tie them logically enough to their respective CSS and JavaScript. It's a loose system though, and having to operate so naively in a global namespace often leaves me craving the rigid control over dependencies and associations which imperative languages offer.

## Custom Elements

Custom Elements are a major part of the Web Components spec which is making its way natively into browsers today. They allow developers to create custom HTML tags, with custom behaviour, isolated inside a "shadow DOM" - its own scope, invisible to any consumer. It involves the creation of an HTML `<template>` and a registration of custom behaviour using `document.registerElement`. Once a component has been created, it allows you to use it with descriptive, semantic markup like this:

```html
<gallery title="Holiday">
  <img src="beach.jpg">
  <img src="sunset.jpg">
  <img src="city.jpg">
</gallery>
```

When this `<gallery>` tag is instantiated, it creates a shadow DOM, and fills it with whatever content has been put in the `gallery` template. For example, the template markup may look like this:

```html
<template name="gallery">
  <style>
    section {
      padding: 10px;
      background: #333;
    }

    .images img {
      display: none;
    }
  </style>
  <section>
    <header></header>
    <div class="images"></div>
  </section>
</template>
```

Notice how simple the selectors can be? No concern needs to be made for global leakage. The title and images would be filled in and controlled with JavaScript.

This freedom to create in a private space gives developers the same flexibility as developing in a closure, for example, when writing modular JavaScript. It doesn't mean Custom Elements follow the 'Angular Approach' of moving all your code in HTML. Custom Elements are initialized in JavaScript and have all the benefits of imperative, reactive code.

By developing in a private shadow DOM, you are allowed the freedom of custom HTML, CSS and JavaScript without the hassle of having to bind together complex classes, data attributes and IDs. Code becomes terse and more readable, and worrying about conflicts with other elements on the page - which is to some degree outside of your control as a developer - becomes a thing of the past.

Custom Elements are a new feature in browsers, which recently made their way into Chrome stable. The [Polymer][polymer] project provides a great polyfill for them for other browsers.

## React

React elements, similar to Custom Elements, are developed in a private scope, but in this case, a single language also - JavaScript. Although alien, writing and using a simple React component may look like this:

```js
class Comment {
  styles = {
    username: {
      fontWeight: 'bold',
      paddingRight: '10px',
    },
    comment: {
      color: '#444',
    },
  };

  render () {
    return (
      <li style={this.styles} onClick={this.handleClick.bind(this)}>
        <span class="username">{this.props.username}</span>
        <span class="comment">{this.props.comment}</span>
      </li>
    );
  };

  handleClick () {
    alert('clicked!');
  };
}
```

```html

<Comment props={{ username: 'richard', comment: 'React!' }} />
```

The HTML style tags are JSX - and can be compiled into regular JavaScript objects, for example by using the [reactify][reactify] Browserify transform.

But we all agreed inline styles and scripts were bad, _right_? I'd argue the benefits of directly, imperatively referencing any styles and UI events directly on a DOM element, rather than through the abstraction of finding, styling or listening to DOM elements by identifiers like classes, outweigh the negatives. React elements are JavaScript objects first, HTML elements second.

The React library takes care of converting them to HTML, rendering them on the page, and updating them on changes. It actually does this better than doing it manually would, as it diffs changed HTML against HTML which is already rendered on the page, and only changes as much as is necessary, rather than rerending the whole element. For example, it might just add or remove a child element, or alter a style.

## Aren't we already close enough?

There are hundreds of open source libraries out there which instantiate and control DOM elements for you. For example there are a myriad of jQuery libraries which allow the creation of custom elements like lightboxes, slideshows and validating forms.

These have many drawbacks though. They are often dependent on DOM manipulation libraries, canonically jQuery, and are often too opinionated about how they should look and behave. At best you get a pluggable API, but generally you get verbose and unintuitive options objects. They also require manual creation in JavaScript, rather than just adding tags to your HTML (or HTML-like) code.

Custom Elements differ in that they allow you to use the three languages which you're already using as they were designed to be used. Using HTML Imports, another part of the Web Components spec, Custom Elements can be imported directly into your pages, rather than having to be instantiated with JavaScript.

```html
<link rel="import" href="/components/gallery.html">

<gallery />
```

Although obviously React demands a dependency, the HTML style syntax means third party components end up being used a similar way.

## What does this mean for open source?

The goal is to have a standardised architecture for reusable, customisable DOM elements. I want to be able to import a component and put it in place as easily as I install a gem, or `require` an NPM module.

I don't think the encapsulation of style is important here. In fact, I often feel UI libraries being particularly opinionated about looks slows me down as a developer. Of course sometimes this makes sense. For example [material-ui][material-ui] includes a huge amount of element styling, but creating elements which look and feel a certain way is the reason it was created.

Libraries which offer elements such as mobile navigation menus or autocompleting text fields ought not tell me how they should look. Their ideas generally conflict with my own ideas, and are often troublesome to override. In these cases I'm far more concerned with having the functionality put in place for me, so I can style it to the look and feel of my site as I choose.

We need to make a good separation of concerns in HTML and CSS the expectation in open source code, and our own code as well. Too many libraries are breaking the Single Responsibility Principle by pulling more than they can carry. The best UI Component libraries are going to be the ones which concern themselves with either functionality or style. Never both.

[luke_inheritance_composition]: https://www.madetech.com/blog/boundaries-in-object-oriented-design
[npm]: npmjs.com
[bower]: http://bower.io/
[browserify]: http://browserify.org/
[amd]: https://github.com/amdjs/amdjs-api/blob/master/AMD.md
[bem]: https://css-tricks.com/bem-101/
[polymer]: https://www.polymer-project.org/1.0/
[reactify]: https://www.npmjs.com/package/reactify
[material-ui]: https://github.com/callemall/material-ui
