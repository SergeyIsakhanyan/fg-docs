### [Home](https://sergeyisakhanyan.github.io/fg-docs/)

# Routing

Routing is the ability to move between different parts of an application when a user enters a URL or clicks an element (link, button, icon, image etc) 
within the application. Originally web applications consisted in interconnected `html documents` that one could navigate through links between them. There is two 
types of routing in `JS`:

- server-side routing
- client-side routing

### server-side routing
Every time a user clicked a link on a website a new document would be generated in the server and sent back to the browser to be rendered in their screen.

### client-side routing
For achieving `client-side rendering` we need to create app/website as `SPA(Single-Page Application)`. SPA's are based on a single document model. 
This means that web applications’ lifespan happens on a single html page, along with the transitions between the different views.

#### How it works
A Javascript router is a piece of software in charge to organize the states of the application, switching between different views.
The router will be in charge of simulating transitions between documents by watching changes on the URL. 
When the document is reloaded or the URL is modified somehow, it will detect that change and render the view that is associated with the new URL.


## Client-side Routing

Client-side routing is handled solely by JavaScript on the page. Whenever a user clicks on a link, the URL bar changes and a different view is rendered on the page. This view could be anything - JSX or HTML.

#### Pros
- Routing between components is fast as the amount of data that renders is less. The rest of the data is rendered by the DOM, and even when there's tons of HTML and CSS to render, the DOM handles that part in the blink of an eye. Using lazy loading, any delay in rendering HTML is compensated for.
- For better user experience, animations and transitions can be easily implemented when switching between different components.
- It gives a real sense of a single-page application in action. No separate pages are rendered, and the current page doesn't refresh to load a new view.

#### Cons
- The initial loading time is considerably large as all the routes, components, and HTML have to be loaded at once when the application first mounts. The whole website or web app needs to be loaded on the first request.
- There is unnecessary data download time for unusable views that cannot be anticipated on the first render of the application.
- It generally requires an external library, which means more code and more dependency on external packages, unlike routing on the server-side.
- Client-side routing and rendering convert JavaScript to HTML, making search engine crawling less optimized.

# React Router

- `react-router`: the core library
- `react-router-dom`: a variant of the core library meant to be used for web applications
- `react-router-native`: a variant of the core library used with react native in the development of Android and iOS applications.

The react-router package includes a number of routers that we can take advantage of depending on the platform we are targeting:
- BrowserRouter
- HashRouter
- MemoryRouter

### BrowserRouter
It uses `history API`, i.e. it's unavailable for legacy browsers (IE 9 and lower and contemporaries). Client-side React application is able to maintain clean routes like `example.com/react/route` but needs to be backed by web server. Usually this means that web server should be configured for single-page application, i.e. same `index.html` is served for `/react/route` path or any other route on server side. On client side, `window.location.pathname` is parsed by React router. React router renders a component that it was configured to render for `/react/route`.  
The `BrowserRouter` is used for applications which have a dynamic server that knows how to handle any type of URL whereas the `HashRouter` is used for static websites with a server that only responds to requests for files that it knows about.

### HashRouter
It uses URL hash, it puts no limitations on supported browsers or web server. Server-side routing is independent from client-side routing.

Backward-compatible single-page application can use it as `example.com/#/react/route`. The setup cannot be backed up by server-side rendering because it's `/` path that is served on server side, `#/react/route` URL hash cannot be read from server side. On client side, `window.location.hash` is parsed by React router. React router renders a component that it was configured to render for `/react/route`, similarly to `BrowserRouter`.  
Most importantly, `HashRouter` use cases aren't limited to SPA.

### MemoryRouter
A router which doesn’t change the URL in your browser instead it keeps the URL changes in memory. It is very useful for testing and non browser environments.
But in browser, It doesn’t have history. So you can’t go back or forward using browser history.


### History
Each router creates a `history` object that it uses to keep track of the current `location` and re-renders the application whenever this location changes.
For this reason, the other React Router components rely on this history object being present: which is why they need to be rendered inside a router.
The `BrowserRouter` uses the [`HTML5 history API`](https://developer.mozilla.org/en-US/docs/Web/API/History_API) to keep the user interface in sync with the URL in the browser address bar.  
The `location` object within the history object is shaped like so:
```
{ pathname, search, hash, state }
```

## Routes

The `<Route/>` component is one of the most important building blocks in the React Router package. It renders the appropriate user interface when the current location matches the route’s `path`.

```
<Route path=”/items”/>

or

<Route exact path=”/items” />
```

First one is matched when the pathname is `/items` or, all other paths that start with `/items/` for example `/items/2`. Second one ensures that only the pathname that exactly matches the current location is rendered.

The `<Route/>` component provides three props that can be used to determine which component to render:
- **component** - defines the React element that will be returned by the `Route` when the path is matched
- **render**    - provides the ability for inline rendering and passing extra props to the element
- **children**  - is similar to the render prop, but element defined by the child prop is returned for all paths whether the current location matches the path or not

```
<Route 
  exact 
  path=”/items” 
  component={Items}
/>

<Route 
  exact 
  path=”/items” 
  render={() => (<div>List of Items</div>)}
/>

const cat = {category: “food”}
<Route 
  exact path=”/items” 
  render={props => <Items {…props} data={cat}/>}
/>

<Route children={props => <Items {…props}/>}/>
```

## Switch
The react-router library also contains a `<Switch/>` component that is used to wrap multiple `<Route/>` components. The Switch component only picks the first matching route among all its children routes.

```
<Switch>
  <Route 
    path=”/items” 
    render={() => (<div><em>List of items</em></div>)}
  />
  <Route 
    path=”/items/2" 
    render={() => (<div>Item with id of 2</div>)}
  />
</Switch>
```

## Link 
The `react-router` package also contains a `<Link/>` component that is used to navigate the different parts of an application by way of hyperlinks. The main difference is that using the Link component does not reload the page but rather, changes the UI.

```
<div>
    Home Component
    <ul>
      <li>
        <Link to=”/items”>Items</Link>
      </li>
      <li>
        <Link to=”/category”>Category</Link>
      </li>
      <li>
        <Link
          to={{ pathname: "/courses", search: "?sort=name", hash: "the-hash", state: { fromDashboard: true } }}
        />
      </li>
      <li>
        <Link to={location => `${location.pathname}?sort=name`} />
      </li>
      <li>
        <Link to="/courses" replace />
      </li>
    </ul>
</div>
```

- **to:** a string representation of the Link location, created by concatenating the location’s pathname, search, and hash properties.
- **to:** an object that can have any of the following properties: 
    - `pathname`: a string representing the path to link to.
    - `search`: a string representation of query parameters.
    - `hash`: a hash to put in the URL, e.g. #a-hash.
    - `state`: state to persist to the location.

## Redirect
The `react-router` package also contains a `<Redirect/>` component which will navigate to a new location. The new location will override the current location in the history stack.

```
<Route exact path="/">
  {loggedIn ? <Redirect to="/dashboard" /> : <HomePage />}
</Route>

<Redirect to={{ pathname: "/login", search: "", state: null }} />
```
```
<Redirect from="/old-path" to="/new-path" />
```

# Nested Routing

### What is nested routing?

Nested route is the route which is child of another route. Nested routing can be thought of multiple forward slash in the URL.  

```
www.organization.com/employees
www.organization.com/employees/:employeeId
www.organization.com/employees/:employeeId/projects
www.organization.com/projects/:projectId
```

```
<Router history={hashHistory}>
  <Route component={App} path="/">
    <Route component={Home} path="/home"></Route>
    <Route component={View1} path="/view1"></Route>
    <Route component={View2} path="/view2"></Route>
  </Route>
</Router>
```

### Why nested routing?

Nested routing is essentioal for url sharing, dynamicity and SEO. URL sharing means that one can reach directly to the desired page with desired data. This will automatically make sure the components and features are implemented to work independently.  

*NOTE:* no extra dependency needed for nested routing.

![](https://miro.medium.com/max/1400/0*VVhTWZ30CkHQHsEJ)

### What can solve nested routing?

There are various techniques to implement layouts, each with their own pros and cons:

- Using Render Props
- Using HOC's
- Nesting routes

```
import React from "react";
import { BrowserRouter as Router, Switch, Route } from "react-router-dom";

// Layout
const Layout = ({ children }) => (
  <div>
    <header>My header</header>
    {children}
    <header>My footer</header>
  </div>
);

// Pages
const PageA = () => <Layout>This is Page A</Layout>;
const PageB = () => <Layout>This is Page B</Layout>;

// Routes
export default function App() {
  return (
    <Router>
      <Switch>
        <Route path="/pageA" component={PageA} />
        <Route path="/pageB" component={PageB} />
      </Switch>
    </Router>
  );
}
```

In case of using render props React will remount the entire layout on every route transition. Another potential issue with this technique is that the Route will always mount the page component regardless of any conditional logic in the Layout.

#### _NOTE:_ In this approach `page` component will always mount before `layout` component.  


```
import React from "react";
import { BrowserRouter as Router, Switch, Route } from "react-router-dom";

// Layout
const Layout = ({ children }) => (
  <div>
    <header>My header</header>
    {children}
    <header>My footer</header>
  </div>
);

// HOC
const withLayout = (Component) => (props) => (
  <Layout>
    {/* All props are passed through to the Component being wrapped */}
    <Component {...props} /> /
  </Layout>
);

// Pages
const PageA = withLayout(() => <p>This is Page A</p>);
const PageB = withLayout(() => <p>This is Page B</p>);

// Routes
export default function App() {
  return (
    <Router>
      <Switch>
        <Route path="/pageA" component={PageA} />
        <Route path="/pageB" component={PageB} />
      </Switch>
    </Router>
  );
}
```

Using HOC's for layout will solve the problem of the `page` component mounting before the `layout` component. Below components hierarchy for using render props and for HOC's:  

```
// render props

Page ↳ Layout ↳ Render prop content
```

```
// HOC

withPage() ↳ Layout ↳ Page
```

This makes the mounting order of the components a bit more sensible.

```
import React from "react";
import { BrowserRouter as Router, Switch, Route } from "react-router-dom";

// Layout
const BackendLayout = ({ children }) => (
  <div>
    <header>This is the admin backend!</header>
    <section>{children}</section>
  </div>
);

// Pages
const ViewUsersPage = () => <>This is a backend page</>;
const ViewBlogpostsPage = () => <>This is another backend page</>;

// Routes
export default function App() {
  return (
    <Router>
      <Switch>
        <Route
          path="/backend"
          render={({ match }) => <BackendRoutes basePath={match.path} />}
        />
        {/* ... additional top-level routes using other layouts ... */}
      </Switch>
    </Router>
  );
}



// Nested backend routes
const BackendRoutes = ({ basePath, username }) => (
  <BackendLayout username={username}>
    <Route path={`${basePath}/users`} component={ViewUsersPage} />
    <Route path={`${basePath}/blogposts`} component={ViewBlogpostsPage} />
    {/* ... additional routes under /backend ... */}
  </BackendLayout>
);
```

As you can see, the whole Route is nested in the Layout. This will indeed prevent the Layout from remounting on page transitions.  


# Dynamic Route URL

```
<Router>
  <div>
    <h2>Accounts</h2>

    <ul>
      <li>
        <Link to="/netflix">Netflix</Link>
      </li>
      <li>
        <Link to="/zillow-group">Zillow Group</Link>
      </li>
      <li>
        <Link to="/yahoo">Yahoo</Link>
      </li>
      <li>
        <Link to="/modus-create">Modus Create</Link>
      </li>
    </ul>

    <Switch>
      <Route path="/:id" children={<Child />} />
    </Switch>
  </div>
</Router>
```

Accessing dynamic path parameter in a URL:
```
this.props.match.params.id
```

Also we can have more than one route parameters:
```
<Route
  exact
  path="/genres/:genreName/:genreId"
  component={GenreList}
/>
```


# Route's Lazy Loading

The concept of lazy loading our React components is really simple. Load the minimal code to the browser that will render a page. Load additional small chunks of code when needed. By loading less JavaScript code to the browser, that will default to better performance and better TTI results.
*TTI is the result of how long does it take for the user to actually be able to interact with the application or site.*

In React for Lazy Loading we will use `React.Lazy` and `Suspense`. The React.lazy function lets you render a dynamic import as a regular component.

```
// Before 
import OtherComponent from './OtherComponent';

// After
const OtherComponent = React.lazy(() => import('./OtherComponent'));

```
`import()` must return a Promise which resolves to a module with a default export containing a React component.
The lazy component should then be rendered inside a Suspense component, which allows us to show some fallback content.

```
<Suspense fallback={<div>Loading...</div>}>
  <Component />
</Suspense>
```

Router level code splitting and Lazy Loading will look like this:

```
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);
```

The Switch component job is to only render a single route component.

# React-Router History object

React-router uses [history](https://github.com/remix-run/history) dependency which provides several different implementations for managing session history in JavaScript in various environments.

- `browser history`: a DOM-specific implementation, useful in web browsers that support the HTML5 history API
- `hash history`: a DOM-specific implementation for legacy web browsers
- `memory history`: an in-memory history implementation, useful in testing and non-DOM environments like React Native

history objects typically have the following properties and methods:
- `length`: (number) The number of entries in the history stack
- `action`: (string) The current action (PUSH, REPLACE, or POP)
- `location`: (object) The current location. May have the following properties:
    - `pathname`: (string) The path of the URL
    - `search`: (string) The URL query string
    - `hash`: (string) The URL hash fragment
    - `state`: (object) location-specific state that was provided to e.g. push(path, state) when this location was pushed onto the stack. Only available in browser and memory history.
- `push(path, [state])`: (function) Pushes a new entry onto the history stack
- `replace(path, [state])`: (function) Replaces the current entry on the history stack
- `go(n)`: (function) Moves the pointer in the history stack by n entries
- `goBack()`: (function) Equivalent to go(-1)
- `goForward()`: (function) Equivalent to go(1)
- `block(prompt)`: (function) Prevents navigation

_**NOTE:**_ **history object is mutable.**



### [History API and Location object](https://sergeyisakhanyan.github.io/fg-docs/HistoryAPI-Location.html)

### [Home](https://sergeyisakhanyan.github.io/fg-docs/)









