### [Home](https://sergeyisakhanyan.github.io/fg-docs/)

# React Lifecycle methods

React lets you define components as classes or functions:
- Functional component is just a plain JavaScript function that returns JSX. 
- Class component is a JavaScript class that extends React.Component which has a render method.

### The only method you must define in a React.Component subclass is called render().

Whenever a `ReactComponent` is changing the state, the `ReactComponent` is converted to the `ReactElement`. Now the `ReactElement` can be inserted to the virtual DOM, compared and updated fast and easily. How exactly - well, that’s the job of the diff algorithm. [For more about `ReactComponent`, `ReactElement` and `Virtual DOM` please click here](https://sergeyisakhanyan.github.io/fg-docs/DOM-VirtualDOM.html).

![React Component Lifecycle Methods](/images/react_component_lifecycle.png "React Component Lifecycle Methods")

### In React, we have four main lifecycle phases.

## React Mount

Mount phase is the initial stage of the React component lifecycle and the moment when React creates our components and inserts them into the DOM.
Let’s see the component mount methods.

### React Constructor

- It’s a component lifecycle method that is fired before the react component is mounted.
- Constructor is useful when we need to init components state, bind functions, or event handlers in our component.
- We always need to remember to call super(props) to avoid situations when our component’s props are undefined. [Your can read here why we need call super(props) here.](https://medium.com/@jbbpatel94/why-do-we-write-super-props-fc367074a2af)

### React static getDerivedStateFromProps

- This method is used in Mount and Update lifecycle.
- This component lifecycle method is called just before the render method in both cases, mounting and updating.
- It’s handy when we would like to change our component’s internal state by recognizing the props’ change implemented into the component. [When to Use Derived State?](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#when-to-use-derived-state)

### [Home](https://sergeyisakhanyan.github.io/fg-docs/)
