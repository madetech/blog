# React and MVC

React is improving the way we build frontends, but I find common patterns are making our apps more complex to write and manage, and more difficult to understand.

I believe this is complicated by the capabilities you give a React component. React components need data to render, like any other view component, and rendering a React component with some data is a simple, synchronous process. This is easy to do on the server:

```js
// Defining the component
const ProfilePage = ({ username, numPosts, numComments }) =>
  <main>
    <h1>{username}</h1>
    <span>{numPosts} Posts</span>
    <span>{numComments} Comments</span>
  </main>

ProfilePage.propTypes = {
  username: PropTypes.string.isRequired,
  numPosts: PropTypes.number.isRequired,
  numComments: PropTypes.number.isRequired
}

// Rendering the component as HTML
ReactDOM.renderToStaticMarkup(
  <ProfilePage
    username="test"
    numPosts={100}
    numComments={400}
  />
)
```

However, a common practice is to fetch this initial data in the component itself, before the render, making the rendering process asynchronous and introducing external API dependencies. For example:

```js
const HomePage = ({ currentUser }) =>
  <main>
    <header>
      <Navigation>
        <NavigationLink to="/profile">
          {currentUser.username}
        </NavigationLink>
      </Navigation>
    </header>
    <article>
      <h1>Hello World</h1>
    </article>
  </main>

HomePage.propTypes = {
  currentUser: PropTypes.shape({
    username: PropTypes.string.isRequired
  })
}

HomePage.getInitialProps = async function () {
  const { username } = await get('/user')
  return { currentUser: { username } }
}
```

This `HomePage` component is not only aware of how to render data, but also aware of how to fetch the data itself. It's dependent on a HTTP API on the same domain, so in order for this component to be rendered, this API has to either be available or mocked out, making testing it more difficult. Traditionally, rendering a view is a synchronous process, the view is given all the data it needs, then is rendered to HTML.

This asynchronous approach means defining API endpoints to return data for individual pages, for example an endpoint to return order data for an OrderShowPage component. This is reasonable enough, but it's often tempting to reuse multiple existing API endpoints to retrieve data for a page. For example, on a basket page you might make an API call to get data on the current order, and a second to get data on related products.

Additionally, all the pages in your application may depend on common data. For example, if you display information on the current logged in user in your navigation bar, you need to fetch this on every page render, or fetch it conditionally depending on whether it's already been fetched, and cache on the clientside. This increases overhead for a developer, and means page rendering becomes dependent not only on a HTTP API, but on a local cache store. Alternatively, common data could be included in every API response, but that leads to non-semantic REST usage.

React is a view layer, it shouldn't force a particular architecture on the rest of your application. By organising a React app this way, you have to build much of your backend as an API. It's a shame to lose the benefits of patterns like MVC because you want to use React on the frontend.

To use an MVC metaphor, I've found complex React page components end up acting as both markup and page controllers. This is a confusing mix and doesn't scale well. The more requests you need to put in the page, the more your page grows, and the slower it renders. You effectively end up reimplementing MVC within the view layer, but with significant overhead.

In MVC frameworks that use HTML, for example Phoenix or Rails, you define routes to map requests to controller actions, where you retrieve all the data needed to render the view. Then you render the HTML using that data and a templating language. It's a simple, synchronous process. Data is retrieved, passed into the view, and HTML is returned. On the server, this all happens in a single request, and the developer doesn't have to make many performance considerations based on where the data is coming from.

We should be able to build React apps that render the same way. We should be able to drop React in as a replacement renderer in any controller, in any language, rather than having to build Node APIs for everything.

## MVC

In recent experiments with this approach, we've been using 'polymorphic' routes which can serve HTML or JSON conditionally. The idea is, when the first page request is made we want to respond with HTML and the JavaScript necessary to take over rendering in the browser. On subsequent requests to the same URLs the client requests JSON instead by passing an `Accept` header.

An example controller action in Node might look like this:

```js
app.get('/basket', async function (req, res) {
  const user = await Session.getCurrentUser()
  const lineItems = await Basket.forUser(user)
  const recommendedItems = await Recommendations.forUser(user)

  res.renderComponent('BasketPage', {
    username: user.username,
    lineItems: lineItems.map(item => ({
      name: item.name,
      quantity: item.quantity,
      price: item.price
    })),
    recommendedItems: lineItems.map(item => ({
      name: item.name,
      image: item.image
    }))
  })
})
```

On an initial page load, so when the Accept header is `text/html`, `res.component.render` would use server side react rendering to render the page as HTML, including the JS client bundle. When the Accept header is `application/json`, it would respond with a JSON payload containing all the data the client needs to render. The `res.component.render` function might look something like this:

```js
function componentMiddleware () {
  return function (req, res, next) {
    res.renderComponent = function (pageName, pageProps) {
      if (this.req.accepts('application/json')) {
        renderJson({ pageName, pageProps })
      } else {
        renderHtml({ pageName, pageProps })
      }
    }

    next()
  }
}
```

An example JSON response would look like this:

```json
{
  "page": "Basket",
  "props": {
    "username": "trustno1",
    "lineItems": [
      { "name": "Pencil", "quantity": 100, "price": "£10.00" }
    ],
    "recommendedItems": [
      { "name": "Water bed", "image": "https://cdn.example.com/img/waterbed-2131244.jpg" }
    ]
  }
}
```

Notice that the single response body includes the data required for the page, no more, no less. This results in a good performance boost over making more than one API call and taking what you need.

The `page` value is the name of a component which was bundled into the client JS application. We define a components index file which exports these, making it simple to match the component name in the JSON payload to the component itself.

```js
export { default as HomePage } from './HomePage'
export { default as AboutPage } from './AboutPage'
export { default as UserProfilePage } from './UserProfilePage'
```

All the client has to do is render that component with the given `props`. We use Redux state to store what component is rendered at the moment, injecting the `initialState` on the initial HTML render using a JavaScript snippet in the HTML, and then updating it with Redux reducers on page transitions and history events.

```js
window.__pageState = {
  page: 'HomePage',
  props: {
    currentUser: {
      username: 'fox'
    }
  }
}
```

## Other languages

Now that we're able to drop React in as an efficient page renderer, separated from the API request paradigm, we'd ideally not have it dependant on a Node.js backend either. Given React is a JavaScript library, server side rendering is only available in Node.js at the moment, but there's no reason rendering has to happen in the same process as the rest of your backend logic.

On some recent and ongoing web applications, we've been running small Node API web servers which expose a single endpoint, something like `POST /render`, which will respond with HTML or JSON conditionally as discussed above. We run this on the same server as our primary backend, whether that's Elixir or Rails, or anything else, and post page data to it in a format identical to the page response JSON above. The node apps look something like this:

```js
const express = require('express')
const bodyParser = require('body-parser')
const { renderJson, renderHtml } = require('./lib/renderer')

const server = express()

server.use(bodyParser.json())

server.post('/render', function (req, res) {
  const { page, props } = req.body

  if (req.accepts('application/json')) {
    renderJson({ page, props })
  } else {
    renderHtml({ page, props })
  }
})

server.listen(3000, () => `Rendering server listening on http://localhost:3000`)
```

By splitting rendering out into a separate program, we're able to use it like any other renderer in any other language. For example, we've built custom renderers in both Phoenix and Rails which call the node app over HTTP.

For example, you can write Rails controller actions like this:

```ruby
def show
  user = User.find(params['id'])
  props = {
    user: {
      username: user.username,
      age: user.age
    }
  }

  render component: { name: 'UserPage', props: props }
end
```

Which would POST data like the following to the node app:

```json
{
  "page": "UserPage",
  "props": {
    "user": {
      "username": "scully",
      "age": 40
    }
  }
}
```

The node app then responds with HTML or JSON, which the Rails app can render as normal.

This way we're able to get the benefits of any language or framework with the benefits of a full featured React frontend. You can simulate framework view features by passing certain props through to the node app by default. For example, on a recent project, we passed flash data and a CSRF token to each render call by merging them in as default props, so every page level component had access to this data.

The biggest downside is React rendering isn't as fast as HTML rendering yet, but it's not that slow either.

## When to do this

Smaller applications won't see most of the benefits of a bespoke approach like this. If you're making a website that's a couple of pages, you'll get the most bang for your buck with an existing framework like Next.js consuming an API.

I think React becomes a more appealing proposition for larger applications when it can be more comfortably dropped into existing stacks. Having to re-architect everything with brand new tools and brand new tech, solely to get the benefits of a frontend library, is often too high risk to be reasonable.

By introducing this abstraction, I think you find a pretty clean separation between your frontend and backend, while remaining pragmatic about their relationship. Your backend is aware of what it's rendering, and where to get the data. Your frontend is aware of where the backend is, and what data it'll give.

We've used this to success on some customer websites, and are keen to see where we can take it in future.
