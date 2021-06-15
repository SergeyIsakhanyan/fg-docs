## Styling in React
- CSS Stylesheet and Classnames
- CSS Modules
- CSS-in-JS / Styled Components
- Inline Styling

### CSS Stylesheet and Classnames - Importing CSS file in Component
We can also create an individual style file for each component and import the style files in the component, we can divide the styling into multiple files and import it as per the requirement in the component. CSS Files are imported in the same way as we import script files.

```
// CSS

.container {
  width: 400px;
  height: 400px;
  background-color: blue;
}
```

```
// Component

export default function MyComponent() {
    return(
      <div className="container">Component Content</div>
    )
}
```

```
import React from 'react';
import './App.css';

function App() {
  return (
      <header className="App-header">
        <p style={{"margin": "1px", "padding": "5px"}}>
          <code>src/App.js</code>
        </p>
        <a style={{"color": "red", "backgroundColor": "green"}}
          className="App-link" href="https://reactjs.org" target="_blank">
          Learn React
        </a>
      </header>
  );
}

export default App;
```

### Advantages of importing CSS in component are:
- Style Files are divided into sub-parts on the basis of components.
- We can have small styling as per each component.
- Style files can be imported dynamically when a component is required.
- Standard CSS files are easy for the browser to optimize.
- Quickly iterate a new design.
- Ease of use for markup specialists.
- Universal - you can easily use the same stylesheet in a React project & a Vue project.

#### Disadvantages of importing CSS in component are:
- Readability.
- Old and complicated CSS files can live on for years.
- Global scope, specificity and cascading nature.
- No true dynamic styling.

In the React ecosystem, we have a lot of different libraries for different purposes, and in the styling part of the frontend it’s the same, we have a lot of libraries and concepts to style our React applications. Here is one of the most used ways to style a React application:


### CSS Modules

A CSS module is just a simple `.css` file, and it renders into the HTML using a dynamic CSS class name. The whole idea of this concept is to avoid name collisions or affecting the styles of other components in our applications:
```
.container_4xks92k2kl {
  width: 400px;
  height: 400px;
  background-color: blue;
}
```

### CSS-in-JS / Styled Components

CSS-in-JS is not a specific library, it’s a concept that tries to solve the problem of styling in React applications.  
That’s the idea that CSS-in-JS introduced to us, instead of passing a lot of class names attributes to our elements, let’s create specific styled-components and benefit from the idea of componentization that React introduced to us:
```
import styled from "styled-components";

const Button = styled.button`
  width: 200px;
  height: 40px;
  background-color: green;
  border-radius: 6px;
`; 
```
**NOTE**: Styled Components takes the actual CSS properties, not camelCased like React inline styling does.

#### Advantages of Styled Components are:
- Automatic critical CSS.
- No class name bugs.
- Easier deletion of CSS.
- Simple dynamic styling.

#### Disadvantages of Styled Components are:
- Polluting the React DOM.
- Workarounds required – you can easily overengineer your app.
- Harder for markup specialists.
- Parses all of the style definitions into plain CSS at build time and drops everything them all into style tags in the head of your `index.html` file.


### Inline Styling

Inline styling is one of the most common ways of styling React applications, a lot of developers start to use this concept when they’re starting a new application because it’s very easy to understand at first and you can achieve the same final result that you would achieve in other concepts like `CSS-in-JS` and `CSS Modules`.  
Inline styling in React is pretty simple:
```
import React from "react";

const styles = {
  width: 200,
  height: 50,
  backgroundColor: 'red'
};

const Button = () => (
  <button style={styles}>My Button</button
)
```
or
```
import React from "react";

const Button = () => (
  <button
    style={{
      width: 200,
      height: 50,
      backgroundColor: 'red'
    }}
  >
    My Button
  </button
)
```

#### Advantages of Inline Styling are:
 - It is especially useful for a small number of style definitions.
 - It can override other style specification methods at the local level.
 - Easy to understand.
 - Easy to start styling.

#### Disadvantages of Inline Styling are:
- It does not separate out the style information from content.
- The styles for many documents can not be controlled from one source.
- They override the existing styles of the component.
- Pseudo Elements and Classes cannot be used together.
- Don't have access to CSS features like pseudoselectors, media queries.
- Not reusable.
- Performance: Inline Styles are slower.

**NOTE 1:** When you’re using inline styling in React, you don’t need to pass a unit to a property in CSS, you can pass just a number and React automatically appends px to your numeric inline style property.  
**NOTE 2:** The properties in our styles object must be camelCase.


## Performance measurements

For testing performance used these configurations:
- 4 different components - div, span, text input and button.
- A big table containing 10 000 rows, each row includes those components.
- Each component has a lot of styles.
- Every test run at least 100 times for every package.

- *First meaningful paint (time when page’s content appeared on the screen) has been calculated with lighthouse.*
- *Render time has been calculated using componentWillMount and componentDidMount while rendering the same table.*

![performance alt text](https://blog.primehammer.com/wp-content/uploads/2017/09/chart.png)


