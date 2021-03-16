# Document Object Model (DOM)

DOM is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document. 
So, while HTML is a text, the DOM is an in-memory representation of this text.

#### The HTML DOM provides an interface (API) to traverse and modify the nodes. It contains methods like `getElementById` or `removeChild`. We usually use JavaScript language to work with the DOM, because… Well, nobody knows why :).

- JavaScript can change all the HTML elements in the page
- JavaScript can change all the HTML attributes in the page
- JavaScript can change all the CSS styles in the page
- JavaScript can remove existing HTML elements and attributes
- JavaScript can add new HTML elements and attributes
- JavaScript can react to all existing HTML events in the page
- JavaScript can create new HTML events in the page for interaction must be used props,state and refs

#### When to Use Refs
There are a few good use cases for refs:
Managing focus, text selection, or media playback.
Triggering imperative animations.
Integrating with third-party DOM libraries.
Avoid using refs for anything that can be done declaratively.
For example, instead of exposing open() and close() methods on a Dialog component, pass an isOpen prop to it.


![alt text](https://miro.medium.com/max/1400/0*wcRPb3x9X4T4oZGA)


# Virtual DOM

First of all - the Virtual DOM was not invented by React, but React uses it and provides it for free.

#### The Virtual DOM is an abstraction of the HTML DOM. It is lightweight and detached from the browser-specific implementation details. Since the DOM itself was already an abstraction, the virtual DOM is, in fact, an abstraction of an abstraction.

- You can think of it as a copy of the DOM, that can be updated without affecting the actual DOM.
- It has all the same properties as the real DOM object, but doesn’t have the ability to write to the screen like the real DOM.
- The virtual DOM gains it’s speed and efficiency from the fact that it’s lightweight.
- In fact, a new virtual DOM is created after every re-render.


## How does updates work in React?
- On the first load, ReactDOM.render() will create the Virtual DOM tree and real DOM tree.
- As React works on Observable patterns, when any event(like key press, left click, api response, etc.) occurred, Virtual DOM tree nodes are notified for props change, If the properties used in that node are updated, the node is updated else left as it is.
- React compares Virtual DOM with real DOM and updates real DOM. This process is called Reconciliation. React uses Diffing algorithm techniques of Reconciliation.
- Updated real DOM is repainted on browser.


## Additional points regarding updates.
- Virtual DOM is pure JS file and light weight, So capturing any update in Virtual DOM is much faster than directly updating on Real DOM.
- React takes a few milliseconds before reconciliation. This allows react to bundle few processes. This increases efficiency and avoids unnecessary reprocessing. Because of this delay we should not rely on this.state.val just after setState().
- React does shallow comparison of props value. We need to handle deep comparison separately, immutable is the most common way to handle it.
