### [Home](https://sergeyisakhanyan.github.io/fg-docs)

# History API

The DOM Window object provides access to the browser's session history through the `history` object.
It exposes useful methods and properties that let you navigate back and forth through the user's history, and manipulate the contents of the history stack.

`history` object is read-only object which provides following methods:

- `back()`
- `forward()`
- `go()`

To move backward through history:

```
window.history.back()
```

To move forward through history:

```
window.history.forward()
```

To move specific point in history:

```
window.history.go(-1) // this will move back one page

window.history.go(1)  // this will move forward one page

window.history.go(0)  // this have the effect of refreshing the page
window.history.go()   // this have the effect of refreshing the page
```

Also we can determine the number of pages in the history stack:

```
const numberOfEntries = window.history.length
```

### history object methods

`history.pushState()` method adds an entry to the browser's session history stack.
```
history.pushState(state, title [, url])
```

`history.replaceState()` method modifies the current history entry, replacing it with the stateObj, title, and URL passed in the method parameters.
```
history.replaceState(stateObj, title, [url])
```

`history.state` property returns a value representing the state at the top of the history stack.
```
const currentState = history.state
```


# Location

The Location interface represents the location (URL) of the object it is linked to.
Both the Document and Window interface have such a linked Location, accessible via `document.location` and `window.location` respectively.
*According to the W3C, they are the same. In reality, for cross browser safety, you should use `window.location` rather than `document.location`.*

### window.location properties

| window.location 	| Returns                                         	|
|-----------------	|-------------------------------------------------	|
| .origin         	| Base URL (Protocol + hostname + port number)    	|
| .protocol       	| Protocol Schema (http or https)                 	|
| .host           	| Domain name + port                              	|
| .hostname       	| Domain name                                     	|
| .port           	| Port Number                                     	|
| .pathname       	| The initial '/' followed by the Path            	|
| .search         	| ? followed by Query String                      	|
| .hash           	| # followed by the Anchor or Fragment identifier 	|
| .href           	| Full URL                                        	|

### window.location methods

| window.location 	| Result                                          	|
|-----------------	|-------------------------------------------------	|
| .assign         	| This method causes the window to load and display the document at the URL specified |
| .replace          | This method does the same as .assign but there is one difference, the current page will not be saved in session History. We won't be able to use back button |
| .reload         	| Reloads the current URL, like the Refresh button. |    

&nbsp;
&nbsp;
&nbsp;
&nbsp;
  
# React Navigation using `window.location`

First of all we need to render component based on `pathname`. The way to do that we need to check if `pathname` is equal to wanted path or not. If they are the same then render corespondent component.

```
// App

import React, { useState } from "react"

import Accordion from "./components/Accordion"
import ColorSelect from "./components/ColorSelect"

const showAccordion = () => {
  if (window.location.pathname === "/") {
    return <Accordion />
  }
}

const showColorSelect = () => {
  if (window.location.pathname === "/color-select") {
    return <ColorSelect />
  }
}

export default () => {
  return (
    <div>
      {showAccordion()}
      {showColorSelect()}
    </div>
  )
}
```

In above code we can see that we have lots of repetitive checkings. Now we can create reusable route component:

```
// Route

const Route = ({ path, children }) => {
  return window.location.pathname === path ? children : null
}
```

Now we can use our `Route` component like this:

```
// App

import React, { useState } from "react"

import Route from "./components/Route"
import Accordion from "./components/Accordion"
import ColorSelect from "./components/ColorSelect"

export default () => {
  return (
    <div>
      <Route path="/">
        <Accordion />
      </Route>
      <Route path="/color-select">
        <ColorSelect />
      </Route>
    </div>
  )
}
```

Next step will be creating `Header` component for navigation. It's just a new component with links.

```
import React from "react";

const Header = () => {
  return (
    <div className="ui secondary pointing menu">
      <a href="/" className="item">
        Accordion
      </a>
      <a href="/color-select" className="item">
        Color Select
      </a>
      <a href="/translate" className="item">
        Translate
      </a>
      <a href="/search" className="item">
        Wiki Search
      </a>
      <a href="/all" className="item">
        All Widgets
      </a>
    </div>
  );
};

export default Header;
```

Then we need to add our `Header` component to `App` component:
```
    ...
    <div>
      <Header />
      <Route path="/">
        <Accordion />
      </Route>
      ...
    </div>
```

This is great but currently the browser is completely reloading the whole page every time we click on one of these nav items. That means we are reloading all our JavaScript and CSS every time we click on a nav link. For preventing page reload we will create new component called `Link`. 
And in that `Link` component we need add click event handler.

```
import React from "react";

const Link = ({ className, href, children }) => {
  // prevent full page reload
  const onClick = (event) => {
    event.preventDefault();
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;
```

Now we need to change the visibility of the URL and the content without actually reloading the page. There is a method built into the browser to manually update the URL: `window.history.pushState()`.


```
import React from "react";

const Link = ({ className, href, children }) => {
  // prevent full page reload
  const onClick = (event) => {
    event.preventDefault();
    window.history.pushState({}, "", href) // added
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;
```

We are successfully updating the URL when we click the Link components now. And now we need to alert our routes that the URL has changed, so that they can update the content in the window. We can do this with another native window method called `window.dispatchEvent()` and a React method called `PopStateEvent()`.

```
import React from "react";

const Link = ({ className, href, children }) => {
  
  const onClick = (event) => {
    // prevent full page reload
    event.preventDefault();
    // update url
    window.history.pushState({}, "", href);

    // communicate to Routes that URL has changed
    const navEvent = new PopStateEvent('popstate');
    window.dispatchEvent(navEvent);
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;
```

Next we need to add custom event, like `click`, and call it `popstate` and to get trigger event every time the URL changes. Then we need to add an event listener to our `Route` component and say that every time event `popstae` occurs we fire the function `onLocationChange()`. Then we need to add cleaner function to clean up the event listener.

```
import { useEffect } from 'react';

const Route = ({ path, children }) => {
    useEffect(() => {
        // define callback as separate function so it can be removed later with cleanup function
        const onLocationChange = () => {
            console.log('Location Change');
        }
        window.addEventListener('popstate', onLocationChange);
        // clean up event listener
        return () => {
            window.removeEventListener('popstate', onLocationChange)
        };
    }, [])

    return window.location.pathname === path
    ? children
    : null;
}

export default Route;
```

Now that the `Route` component can detect URL change it needs to re-render itself. Because React component re-renders itself every the state is changing, we are going to add `currentPath` to our state and update it every time the URL changes.

```
import { useEffect, useState } from 'react';

const Route = ({ path, children }) => {
    // state to track URL and force component to re-render on change
    const [currentPath, setCurrentPath] = useState(window.location.pathname);

    useEffect(() => {
        // define callback as separate function so it can be removed later with cleanup function
        const onLocationChange = () => {
            // update path state to current window URL
            setCurrentPath(window.location.pathname);
        }

        // listen for popstate event
        window.addEventListener('popstate', onLocationChange);

        // clean up event listener
        return () => {
            window.removeEventListener('popstate', onLocationChange)
        };
    }, [])

    return currentPath === path // updated
    ? children
    : null;
}

export default Route;
```


### [Home](https://sergeyisakhanyan.github.io/fg-docs)
