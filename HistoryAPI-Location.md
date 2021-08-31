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

| window.location 	| Result                                          	|
|-----------------	|-------------------------------------------------	|
| .assign         	| This method causes the window to load and display the document at the URL specified |
| .replace          | This method does the same as .assign but there is one difference, the current page  |
|                   | will not be saved in session History. We won't be able to use back button           |
| 


