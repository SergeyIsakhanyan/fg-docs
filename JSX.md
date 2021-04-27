# React JSX

- JSX stands for JavaScript XML (or JavaScript Syntax eXtension)
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

### How is JSX get compiled?

JSX is not valid JavaScript, web browsers cant read it directly. So, if JavaScript files contains JSX, that file will have to be transpiled. That means that before the file gets to the web browser, a JSX compiler will translate any JSX into regular JavaScript.
JSX produces React Elements.  
There’s an abstraction layer between JSX and what’s actually going on in React land. This abstraction layer is that JSX is always going to get transpiled to `React.createElement()` invocations (typically) via Babel. We will not typically invoke `React.createElement()` directly if we are using JSX.  
```
const element = (
  <MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
);

// Will be converted to plain JavaScript like so.

var element = React.createElement(
  MyButton,
  { color: "blue", shadowSize: 2 },
  "Click Me"
);
```

```
<div>
  <img src="profile.jpg" alt="Profile photo" />
  <h1>Welcome back Paul</h1>
</div>


// The transpiled JavaScript will be:

React.createElement(
  "div",
  null,
  React.createElement("img", { src: "profile.jpg", alt: "Profile photo" }),
  React.createElement(
    "h1",
    null,
    "Welcome back Paul"
  )
);
```

#### Events in JSX

```
var clickhandler = function clickhandler() {
    console.log('you clicked');
  };

var reactNode = React.createElement(
    'div',
    { onClick: clickhandler },
    'click'
  );

ReactDOM.render(reactNode, document.getElementById('app'));


// Now writing the same code using JSX

var clickHandler = function clickhandler() {
    console.log('you clicked');
  };
  
var reactNode = <div onClick={clickHandler}>click</div>;

ReactDOM.render(reactNode, document.getElementById('app'));
```

[More about `React.createElement()`.](https://reactjs.org/docs/react-api.html#createelement)  
[Read about React Elements here.](https://github.com/SergeyIsakhanyan/fg-docs/blob/main/DOM-VirtualDOM.md#reactelement-vs-reactcomponent)  
[Checkout online Babel compiler here.](https://babeljs.io/repl/#?browsers=&build=&builtIns=false&corejs=3.6&spec=false&loose=false&code_lz=DwWQngQgrgLjD2A7ABAY3gG3gJwLwCIAjDKAU32QGcALAQwBN4B3AZQEsAvU3AbwCYAvgD4AUMmQBhDG1QBrZCFIjgAenDQ4SIUA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=es2015%2Creact%2Cstage-0&prettier=true&targets=&version=7.13.17&externalPlugins=)  

### Differences Between JSX and HTML

- Tag attributes are camel cased. `maxlength` in HTML becomes `maxLength` in JSX.
- All elements must be balanced. Tags such as `<br>` and `<img>`, which don’t have ending tags, need to be self-closed. So, instead of `<br>`, use `<br/>` and instead of `<img src="...">`, use `<img src="..." />`.
- The attribute names are based on the DOM API, not on the HTML language specs. When interacting with the DOM API, tag attributes may have different names than those you use in HTML. One of such example is `class` and `className`. `<div class="some-class"></div>` in HTML becomes `<div className="some-class"></div>` in JSX.



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











