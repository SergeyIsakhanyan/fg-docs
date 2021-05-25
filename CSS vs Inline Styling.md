### Styling in React
- CSS Stylesheet
- CSS Modules
- CSS-in-JS
- Inline Styling

## CSS

CSS is the language we use to style a Web page. For using CSS we had to create a separate `.css` file, link our new CSS file by using the link tag in our HTML document, and after this, we had our CSS styling working fine. CSS class example:
```
.container {
  width: 400px;
  height: 400px;
  background-color: blue;
}
```
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

### CSS-in-JS

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

**NOTE 1:** When you’re using inline styling in React, you don’t need to pass a unit to a property in CSS, you can pass just a number and React automatically appends px to your numeric inline style property.  
**NOTE 2:** The properties in our styles object must be camelCase.

#### Pros of Inline Styling
- Easy to understand.
- Easy to start styling.


#### Cons of Inline Styling
- Don't have access to CSS features like pseudoselectors, media queries.
- Not reusable.
- Performance: Inline Styles are slower.
