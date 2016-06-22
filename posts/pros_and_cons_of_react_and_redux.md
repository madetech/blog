# Pros and Cons of React + Redux

React is a JavaScript library which brings a declarative class driven approach to defining UI components. Redux is a state management layer which allows you to write events as simple 'action' objects, and centralises their storage and all change processing. Action objects which look like the following are dispatched in a fire-and-forget fashion and trigger an efficient re-render if necessary.

```js
{ type: 'ADD_COMMENT', comment: { body: 'test comment', user: 1 } }
```

## Pros
### Easy to start writing (if you can get over the syntax)

Writing React templates is extremely similar to writing HTML with interpolation thanks to JSX. It ends up looking similar to Mustache templates, except the markup is directly in your JavaScript component code. For example, a simple "call to action" button might look like this:

```js
import React from 'react'
import style from './style.css'

export default class CTAButton extends React.Component {
  render () {
    return (
      <a href={this.props.href} style={style}>
        <h3>{this.props.title}</h3>
        <span>{this.props.body}</span>
      </a>
    )
  }
}
```

You'd use it like this:

```js
<CTAButton title="Shop Now" body="While stocks last!" href="/shop" />
```

It's unusual, and many developers have a hard time getting used to it, but once you get over your preconceptions it becomes extremely familiar.

Notice that in the above code the markup is inside your JS class, and your css is `import`ed at the top as well. Naturally, your JavaScript code would go here too. React is extremely unusual in that it encourages you to put all your markup, style and functionality in the same place, but this gives you convenience and extreme modularity in the long run, which we know is a good thing.

### Total separation of data and presentation

React provides little more than a presentation layer. Although React components do have a concept of 'state', this is best used for ephemeral storage. Anything you could lose on a new render can go in React state, although when combined with Redux, putting as much of your data in your Redux store as possible generally gives the best results, as it allows complete separation of state (Redux's concern) and presentation (React's concern.) You hook top level React components (think 'views' in an MVC framework, often referred to in the React world as 'containers') to a subset of the data in your Redux store. For example, a 'TweetDash' container might depend on the 'tweets' key in a Redux store with a state like this:

```js
{
  tweets: [
    { text: 'Interested in #ContinuousDelivery? Check out our new book!', user: 'madetech_com' },
    { text: 'Join us tomorrow night for #QuizBuzz, a code-themed pub quiz - free to enter, prizes to win, food & drink provided', user: 'madetech_com' },
    { text: 'Overstacked? The journey to becoming a full stack developer: https://t.co/cwEqxPM1sE', user: 'madetech_com' }
  ]
}
```

```js
import React from 'react'
import { connect } from 'react-redux'
import store from './store'
import TweetList from '../components/TweetList'

class TweetDash extends React.Component {
  render() {
    return (
      <section>
        <h1>Dashboard</h1>
        // The 'tweets' section of state is passed to the component as a 'prop'
        // You can pass this data down to sub-components
        <TweetList tweets={this.props.tweets} />
      </section>
    )
  }
}

function mapStateToProps(state) {
  // Redux diffs this against the full state internally to determine
  // which parts of the state this component needs. It'll only re-render
  // this component when these parts of the state change.
  return { tweets: state.tweets }
}

export default connect(mapStateToProps)(TweetDash)
```

### Never think about re-rendering!

The benefit of this separation of concerns is you don't have to concern yourself with whether something has been rendered before, or whether it's the first time. Since React rendering is immutable, the first render and the 100th render of the same component are handled the exact same way. When state changes, Redux re-renders relevant components on the page.

Users of frameworks like Backbone or Angular may have experience with re-rendering on data changes on the front-end. It's not a new concept. The reason React is _much_ more successful in this regard is because it applies changes to a 'Virtual DOM' and creates a diff of the smallest changeset possible, which it then applies to the DOM. Since updating the DOM is the lengthiest part of the render process, this massive reduction in DOM updates greatly improves performance. It means you really can forget about the rendering process, which has never been true before in front-end.

### DOM binding isn't our concern

If you've written _any_ front-end component, with or without a framework, in the past five years then you know the pain of binding DOM elements to functionality. Imagine a simple comment list with a form. When you add a comment using the form, it appears in the list. Behind the scenes in most implementations, this means listening to forms with a certain class. When one submits you retrieve the content of the form and make an AJAX request to your server with that payload. When it responds you either render the whole form again or render another `<li>` with your templates and append it to the list. This is a very tightly coupled and complex series of operations. Although as web developers, we're quite used to writing them, we write it differently to most of the code we write. In other areas we strive for DRY, reusable code with single responsibilities. But in front-end, we write highly specialised, tightly coupled, multi-responsibility code to achieve simple tasks.

Although React would handle this in much the same way, it would be split across multiple areas of the code with single responsibilities. From the React developers perspective, we have the form element selection (React does this), the form event listening (our Component does this), the AJAX request (a Redux Action), the state updates (a Redux Reducer) and the rendering (React-Redux does this). No more tightly coupled code. No more defining awkward, un-semantic classes in your HTML to suit your JavaScript. Elements are bound directly to functionality.

```js
class LikeButton extends React.Component {
  render () {
    const text = this.props.liked ? 'Unlike' : 'Like'

    return (
      <button onClick={::this.handleClick}>
        {text}
      </button>  
    )
  }

  handleClick (e) {
    e.preventDefault()

    // Proxy the onClick event to the component using this component.
    // This is quite common when building re-usable components.
    this.props.onClick(!this.props.liked)
  }
}

<LikeButton liked={true} onClick={::console.log} />
```

### Server-side rendering

Some of the most touted problems with Single Page Applications (SPAs) are SEO optimisation and page load times. If the client does all the heavy lifting then the user has to wait for initial page load, then for rendering. This is slow. What about accessiblity concerns? There are still users with JavaScript disabled! These issues have always plagued SPAs and there have never been great solutions. Although many have allowed some presentation reuse between server and client, generally using shared template files, the construction around them has always differed. Having to write separate views for the server and the client is unreasonable these days. Since React is just a component library, it can be rendered both in the browser using the DOM, and to a string of HTML which the server can deliver. Using component routing libraries (namely react-router or react-router-redux) means you can even use the same routing on the server and the client. Naturally this is easiest with a Node server, as it's in the same language, but there is support in most other backend frameworks for doing the same, often by running a Node server on the side exclusively for React rendering.

### React isn't a framework

React is a library which provides a declarative method of defining UI components. ReactDOM is an associated library which provides rendering and DOM diffing. Redux is a library which provides a data store, and React-Redux provides the glue between React and Redux. There's a philosophy around building React apps, which I've covered, but there isn't a formal framework to stop you doing what you like with the rest of the app. This reduces lock-in, as you can swap out the presentation layer of your front-end if you change your mind without affecting the rest of your codebase. Changing the data layer is harder, but doable. Conversely, it means React components can be gradually introduced to a codebase, rather than thrown in whole cloth. Facebook did this, replacing existing UI components on the Facebook Wall with React components one by one.

## Cons
### React isn't a framework

Philosophy is great, but when you need to get something done quickly, the React Way can be frustrating. If you have clients and projects and pressing deadlines and the first page of your React handbook no longer works - have actually seen this - you can get frustrated.

Fast change generally means growth and improvement, which is great in plenty of ways. Despite React being a relatively new tool in the front-end toolbox, it's achieved dramatic improvement since it was revealed. You can use it stably in production and your speed of development can flourish, but with a serious caveat. Getting started is _slow_ unless you know what you're doing. React (and JavaScript in general) doesn't have "stable" the same way most languages, libraries or frameworks have "stable". Stability in React is all too often "working well but we better keep these versions locked down because it's all going to change soon."

Be prepared to watch libraries grow from gists to large codebases quickly, and for them to change into something just as confusing by the time you've finally gotten your head around them. Take react-router, which handles client-side routing. It has seen dramatic, unwieldy changes from v0.13.1, v1.0.0, v2.0.0, it's fork rrtr to its child library react-router-redux in the past six months, and coming in fresh it's still hard to pick up where to start. What's the right way to write react-router? What's the write way to write React in general?

The looseness with which React can be employed is great for experimentation, but challenging when you're trying to do things the _right_ way. Knowing there isn't one yet will save you some time here.

### Community conventions are still developing

How do I structure this? How do people handle that?

I won't say library developers don't have strong opinions on how their libraries should be used, because they certainly do. The problem is turnover and change is so rapid, these don't have time to solidify into common practices. Only those really paying attention to monthly, weekly, daily changes in the React community could tell you the best way to use X library.

This is endemic of a larger problem in the JavaScript community. There's so much going on and so many problems to solve, the community hasn't had time to settle on solid, fundamental JavaScript project practices. Some of this is again philosophical, the community certainly favours the \*nixy 'simple functions and common interfaces over rigid structure and adherence to whats popular' standard more than most web developers.

### Build tools are necessary (or strongly encouraged)

For all front-end apps but the absolute simplest, decent build tools are highly recommended. For simple apps you can often get away with shell scripts in your `package.json` file.

```json
{
  "scripts": {
    "start": "webpack-dev-server -d --history-api-fallback --hot --inline --progress --colors --port 3000",
    "build": "NODE_ENV=production webpack --progress --colors"
  },
}
```

For more complex apps, you might want to use a tool like Gulp to manage multiple tasks. These build tools are useful but remain unnecessarily complex. I would strongly recommend sticking to npm scripts like above and using the command line interfaces of your build tools, for example `browserify` or `webpack-dev-server`.

Using build tools isn't too much of a pain, we generally use them when we work in other languages anyway. The only real issue with using them in JavaScript is there aren't standard, reusable solutions for all of your projects. This can unfortunately seriously increase the amount of time it takes to get the idea in your head into code.

### Conclusion

React is an unbelievable way to write front-end code. Once your project is set up and you have a decent idea of what you're doing, developers are able to create stable, snappy and sane applications in a fraction of the time it normally takes. This is especially true when creating single page applications, which have always been a bit of a pain. React introduces a few headaches, learning it up front is challenging and keeping up is more so, but it will save you many, many headaches in the long run.
