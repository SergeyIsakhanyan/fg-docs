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
    </ul>
</div>
```

## Redirect
The `react-router` package also contains a `<Redirect/>` component which will navigate to a new location. The new location will override the current location in the history stack.

```
<Route exact path="/">
  {loggedIn ? <Redirect to="/dashboard" /> : <HomePage />}
</Route>

<Redirect
  to={{
    pathname: "/login",
    search: "",
    state: {}
  }}
/>
```
```
<Redirect from="/old-path" to="/new-path" />
```
















