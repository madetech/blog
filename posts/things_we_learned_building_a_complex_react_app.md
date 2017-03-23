# Things We Learned Building a Complex React App

React is a fantastic tool for building frontends. We've been using it for small applications for a while, and recently used it for a more complex app. Given the library, and the mass of libraries you'll use with it, are still brand new, we encountered many architectural and code challenges throughout development which haven't been solved before.

Making these decisions was a lot of fun, but also created a fair share of headaches. Assumptions we made at the start of the project were challenged strongly later in development. Following are some decisions we've regretted, and a few sins we committed.

## Use Smart Components where you need them

A common pattern in React apps is having top level "smart components", often referred to as "containers", which are the only components which make state changes, through HTTP calls, dispatching Redux actions, or whatever. The benefits of this approach are that very few of your components have to be aware of receiving data and sending data changes. This simplifies the rest of the components, "dumb components", which are just rendering markup based on their props. Separating "smart" and "dumb" components is essential, but I've found prop delegation becomes confusing to read, tedious to write and difficult to manage if you only place your smart components at the top. Page level containers have to be aware of everything every component beneath them could possibly want, and have to provide deep dependency injection to allow all of these components to make data changes, and use sourced data. You end up passing a huge number of props up and down the "tree".

For example, consider a `ContactForm` component inside a `Sidebar` component, which in turn is inside a `HomePage` container. When submitting `ContactForm` an AJAX request should be made to an endpoint on the server. If `HomePage` is the only smart container, then it's the only component capable of making this request. However, the form button is inside the `ContactForm`, so registering the button click event happens there. In practice, it means function props for handling the button click have to be passed from the HomePage container to the ContactForm component, through all intermediary props. For (a contrived and trimmed) example:

```js
@connect(...)
class HomePage extends React.Component {
  handleContactFormSubmission (e) {
    e.preventDefault()
    const formData = { ... }
    this.props.dispatch(submitContactForm(formData))
  }

  render () {
    return (
      <main><h1>Welcome!</h1></main>
      <Sidebar onContactFormSubmission={::this.handleContactFormSubmission} />
    )
  }
}

class Sidebar extends React.Component {
  render () {
    return (
      <div styleName="sidebar">
        <ContactForm onSubmit={::this.props.onContactFormSubmission} />
      </div>
    )
  }
}

class ContactForm extends React.Component {
  render () {
    return (
      <form onSubmit={::this.props.onSubmit}>
        <input type="text" name="name">
        <textarea name="message" />
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

I strongly believe separating components into "those which can access and manipulate state" and "those which can only receive props and _only_ contain markup" is the most sensible approach, but since working on this project I'm against keeping all the data manipulation at the top. I much prefer a structure like this:

```js
class HomePage extends React.Component {
  render () {
    return (
      <main><h1>Welcome!</h1></main>
      <Sidebar />
    )
  }
}

class Sidebar extends React.Component {
  render () {
    return (
      <div styleName="sidebar">
        <ContactFormWidget />
      </div>
    )
  }
}

@connect(...)
class ContactFormWidget extends React.Component {
  handleSubmission (e) {
    e.preventDefault()
    const formData = { ... }
    this.props.dispatch(submitContactForm(formData))
  }

  render () {
    return (
      <form onSubmit={::this.handleSubmission}>
        <input type="text" name="name">
        <textarea name="message" />
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

Now, the `ContactForm` widget is entirely responsible for its own state manipulation, meaning `HomePage` and `Sidebar` don't have to take responsibility for any part of its internal implementation. Not having to wire every component all the way to the top of the application greatly improves development speed, increases the portability of `ContactForm`, makes it simpler to test, and improves the speed of refactoring across all the components involved.

## Don't split your backend into multiple servers

Splitting your API server out from your rendering server is a reasonably common pattern in React development at the moment. The most popular React boilerplate does it. It sounded pretty good in theory, one server would be a pure RESTful API written in Node, proxying requests to our Rails e-commerce backend. The other would match routes for any request that came in and render React server side, so we get the benefits of server side rendering. This meant the rendering server consumes the API server for data on the initial page load, and from that point the client would make requests to the API directly. We wanted that separation of concerns, it sounded awesome.

The separation of concerns got pretty much destroyed when we came to authentication though. We stored user data in signed cookies, so naturally weren't able to use this to form API routes. Instead to allow authorised requests we needed the API to be stateful, and able to send signed cookies to it. We could have proxied those API requests through the rendering server, added authentication to that instead and created proxy routes for all of our API routes. This would have meant pretty much doubling up on all the API code and making two requests for every one we needed.

Having two separate servers meant both had to make compromises for the sake of security and development speed, and really complicated our error handling code. The backend would have been much better off as a single stateful application.

## Don't do too much inside your components

We have both client and server side rendering in the application. We dispatch HTTP requests through Redux actions when rendering a page level component, to fetch the data required to render the page. We used redux-connect to ensure all of these requests were complete before actually rendering, so page renders feel fast and don't have any pop in as it populates. This worked really well, but meant having complex code to manage it in both the server and the client. Additionally, it made testing page level components needlessly complex. Since HTTP requests are being made, we had to either mock these or run them against a dev or staging server in our test suite, when all we really wanted to do was test that the component had certain contents when given certain data.

It would have been much simpler to test if we had changed the rendering process on the server and the client, so that HTTP requests were made before the containers themselves were instantiated, rather than making the container gather their own data. This would have given us a straightforward, synchronous component rendering process. You should use feature testing for integration and interaction, and container tests with a tool like Enzyme to test contents.

## CSS probably isn't worth it

We used CSS in this project rather than inline styles, wanting to try out CSS Modules and PostCSS and thinking it would allow us greater flexibility over our styles. We included several style loaders in our webpack config so we could `import` the CSS files within our components and mix them in with the `react-css-modules` decorator, and used webpack-isomorphic-tools to serve chunked assets in development and bundled assets in production.

It worked well enough throughout most of the development, it wasn't until we had to introduce multiple themes for different markets that we encountered a **ton** of issues with the approach. For example, you'd have to define multiple webpack configurations for each theme and embed conditionals relating to webpack-isomorphic-tools all across your application in order to switch the theme used when rendering the page, and this behaviour would be very awkward to test. We ended up spinning up multiple versions of the app in both development and production, each of which served a different theme. Additionally, we had to litter our CSS with selectors like `:global(.theme-blue) & {}` in order to tweak the designs of different pages differently.

It would have been preferable to define CSS in JS inside our React components instead, using a library like Radium, Glamor, or a litany of others. This would have allowed us to easily switch out values based on props, or even define multiple presentational components for each theme, which would have not only made our code a lot cleaner, but easier to run and deploy.

## You should use React

The user experience is phenomenal in a well built React app, the development experience at its best is too. The community hasn't grown enough to have good, conventional solutions to plenty of problems yet, but it's getting better. There are well known pain points, and plenty of niche ones you'll discover yourself, but this leaves you room for innovation.

<!-- ## Use proper dependency injection -->

<!-- ## Establish proper boundaries and use simple prop structures, for your sanity's sake / Maintain synchronous rendering -->

<!-- ## Keep component parity with server, client and test environments. Otherwise leads to brittle tests and different implementations in each -->

<!-- ## xxx localisation -->

<!-- ## Feature testing is hard -->

<!-- ## Use context over direct dependency references in components when using complex helpers -->
