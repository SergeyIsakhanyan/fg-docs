# React JSX

- JSX stands for JavaScript XML
- JSX allows us to write HTML in React
- JSX produces React “elements”

JSX is an XML/HTML-like syntax used by React that extends ECMAScript so that XML/HTML-like text can co-exist with JavaScript/React code.
The syntax is intended to be used by preprocessors (i.e., transpilers like Babel) to transform HTML-like text found in JavaScript files into standard 
JavaScript objects that a JavaScript engine will parse.

Unlike the past, instead of putting JavaScript into HTML, JSX allows us to put HTML into JavaScript.  
You can think of JSX as a shorthand for calling `React.createElement()`.

```
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### General points

- Less technical people can still understand and modify the required parts. CSS developers and designers will find JSX more familiar than JavaScript alone. I.e., HTML markup looks like HTML markup.
- You can leverage the full power of JavaScript in HTML and avoid learning or using a templating language. JSX is not a templating solution. It is a declarative syntax used to express a tree structure of UI components.
- By adding a JSX transformation step you'll find errors in your HTML you might otherwise miss.
- JSX promotes the idea of inline styles. Which can be a good thing.
- JSX is a separate thing from React itself. JSX does not attempt to comply with any XML or HTML specifications. 
JSX is designed as an ECMAScript feature and the similarity to XML/HTML is only at the surface (i.e., it looks like XML/HTML so you can just write something familiar).
- User-Defined Components Must Be Capitalized.


## JSX vs JS

```
let element = React.createElement('h1', {}, 'This is JavaScript')
```

```
let element = <h1>This is JSX</h1>
```











