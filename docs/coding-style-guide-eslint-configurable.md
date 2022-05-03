
# Coding Style Guide (ESLINT configurable)

## Table of Contents

 - **ESLint** configurable
   - [**Basic**](#basic)
   - [**Operators**](#operators)
   - [**Bad and Good Practices**](#bad-and-good-practices)
   - [**Naming**](#naming)
   - [**Quotes**](#quotes)
   - [**Spacing**](#spacing)
   - [**Props**](#props)
   - [**Refs**](#refs)
   - [**Parentheses**](#parentheses)
   - [**Tags**](#tags)
   - [**Components**](#components)
   - [**JSX**](#jsx)

&nbsp;
&nbsp;

## Basic

* Only include one React component per file (`eslint: react/no-multi-comp`).
* Always use JSX syntax (`eslint: react/jsx-filename-extension`).

&nbsp;
&nbsp;

#### **[Back to top](#table-of-contents)**

## Operators

* **Equality operator**
  - Always use `===` equality, don't use `==` equality (`eslint:eqeqeq`).
    ```javascript
    //bad
    const a = "bad"
    const b = "another bad"
    if(a == b){
      console.log("bad practice")
    }

    //good
    const a = "good"
    const b = "another good"
    if(a === b){
      console.log("good practice")
    }
    ```
* **Operator shorthand**
  - Always use shorthand operators (`eslint:operator-assignment`)
    ```javascript
      //bad
      x = x + y;
      x = y * x;

      //good
      x += y
      x *= y
    ```

#### **[Back to top](#table-of-contents)**

## Bad and Good Practices

* **Functions**
  - Don't use `alert`, `confirm`, `prompt` functions (`eslint:no-alert`).

    ```javascript
      //bad
      alert("here!");
      confirm("Are you sure?");

      //write youre custom alert function 
      //good
      customAlert("Something happened!");
      customConfirm("Are you sure?");
    ```
  - Always use `arrow functions` for callbacks (`eslint:prefer-arrow-callback`)
    ```javascript
      //bad
      foo(function(a) { return a; })

      //not arrow but OK
      foo(function*() { yield; }); // generator as callback

      //good
      foo(a => a)
    ```
* **Import & Export**
  - Always define `import` from the new line (`eslint:import/newline-after-import`).
  - Rule for reporting use of an exported name as the locally imported name of a default export (`eslint:import/no-named-as-default`)

* **Conditions & Loops**
  - If an `if` block contains a `return` statement, the `else` block becomes unnecessary. Its contents can be placed outside of the block. (`eslint:no-else-return`).
    ```javascript
      //bad
      function foo() {
          if (x) {
              return y;
          } else {
              return z;
          }
      }

      //good
      function foo() {
          if (x) {
              return y;
          }

          return z;
      }
    ```
    [**More examples for this rule**](https://eslint.org/docs/rules/no-else-return#no-else-return)
  - Always use `default` in `switch` statements. if don't `default` case in your logic write comment `//no default` (`eslint:default-case`).
    ```javascript
      //bad
      switch (a) {
        case 1:
          console.log("bad practice")
        break;
      }

      //good
      switch (a) {
        case 1:
          console.log("bad practice")
        break;
        //no default
      }

    ```

* **Object properties**
  - Always use `object` shorthand syntax (`eslint:object-shorthand`).
    ```javascript
      //bad
      const foo = {
        x: x,
        y: y,
        z: z,
      };

      //bad
      const foo = {
        a: function() {},
        b: function() {}
      };

      //good
      const foo = {x, y, z}

      //good
      const foo = {
        a() {},
        b() {}
      };
    ```
  - Always use `dot-notation` for access `object` properties (`eslint:dot-notation`)
    ```javascript
      //bad
      const x = obj["bar"]

      //good
      const x = obj.bar

      //good
      const x = obj[bar] 
      // Property name is a variable, square-bracket notation required
    ```
#### **[Back to top](#table-of-contents)**

## Naming

* **Variable Naming:**
  - Always use `let` or `const` to declare variable (`eslint: no-undef, prefer-const`).
  - Use one `const` or `let` declaration per variable or assignment.
    ```javascript
    // bad
    const test = 'test',
    isTest = true,
    testCount = 5

    // Good
    const test = 'test'
    const isTest = true
    let testCount = 5
    ```
  - Group all your `const`s and then group all your `let`s.

    ```javascript
    // Bad
    const test = 'test'
    let testCount = 5
    const isTest = true
    let isAvailable = false

    // Good
    const test = 'test'
    const isTest = true
    let testCount = 5
    let isAvailable = false
    ```
  - Don't chain variable assignments (`eslint: no-multi-assign`).

    ```javascript
    // Bad
    let a = b = c = 1

    // Good
    let a = 1
    let b = a // let b = 1
    let c = a // let c = 1 or let c = b
    ```
  - Don't reassign function parameters (`eslint:no-param-reassign`)
    ```javascript
      //bad
      function foo(bar) {
        bar = 13;
      }

      //bad
      function foo(bar) {
          bar++;
      }

      //bad
      function foo(bar) {
        for (bar in baz) {}
      }
      
      //bad
      function foo(bar) {
          for (bar of baz) {}
      }

      //good
      function foo(bar) {
        const baz = 13 
      }

      //good
      function foo(bar) {
          for (anotherBar of baz) {}
      }
    ```
  - Don't declare unused variables (`eslint: no-unused-vars`).
  - Avoid using single letter variables in functions.
    ```javascript
    // Bad
    const name = names.find(n => n === 'John')

    const content = productList.map(p => (
      <div>
        <p>{p.name}</>
        <p>{p.type}</>
      </div>
    ))


    // Good
    const name = names.find(item => item === 'John') // nameItem, nameObj

    const content = productList.map(productItem => ( // productObj
      <div>
        <p>{productItem.name}</>
        <p>{productItem.type}</>
      </div>
    ))
    ```
* **Function Naming:**
  - Do not use trailing or leading underscores (`eslint: no-underscore-dangle`).
    ```javascript
    // Bad
    const _getName = () => {
      // ...
    }

    const getName_ = () => {
      // ...
    }

    // Good
    const getName = () => {
      // ...
    }
    ```
    #### **[Back to top](#table-of-contents)**
    
## Quotes
* **Strings:** 
  - Never use eval() on a string (`eslint: no-eval`).

#### **[Back to top](#table-of-contents)**

## Spacing

- Always include a single space in your self-closing tag (`eslint: no-multi-spaces, react/jsx-tag-spacing`).

  ```javascript
  // Bad
  <Example   />

  // Bad
  <Example 
   />

  // Good
  <Example />
  ```
- Do not pad JSX curly braces with spaces (`eslint: react/jsx-curly-spacing`).

  ```javascript
  // Bad
  <Example name={ name } />

  // Good
  <Example name={name} />
  ```

- Spacing in a function signature (`eslint: space-before-function-paren, space-before-blocks`).
  ```javascript
  // Bad
  const f = function(){}
  const f = function (){}

  const f=()=>{}
  const f= () =>{}

  // Good
  const f = function () {}
  const f = () => {}
  ```
- Avoid spaces between functions and their invocations (`eslint: func-call-spacing`).
  ```javascript
  // Bad
  getFullName ()

  // Bad
  getFullName
  ()

  // Good
  getFullName()
  ```

- Spacing in generators (`eslint: generator-star-spacing`).
  ```javascript
  // Bad
  function * exampleOne() {}
  const exampleTwo = function * () {}

  // Good
  function* exampleOne() {}
  const exampleTwo = function* () {}
  ```
- Spacing in arrays (`eslint: array-bracket-spacing`).
  ```javascript
  // Bad
  const numbersArr = [ 1, 2, 3 ]
  const firstNum = numbersArr[ 0 ]

  // Good
  const numbersArr = [1, 2, 3]
  const firstNum = numbersArr[0]
  ```
- Spacing in objects (`eslint: object-curly-spacing`).
  ```javascript
  // Bad
  const user = {firstName:'John',lastName:'Lennon'}

  // Good
  const user = { firstName: 'John', lastName: 'Lennon' }

  // Good
  const user = {
    firstName: 'John',
    lastName: 'Lennon'
  }
  ```
- Enforce spacing between keys and values in object literal properties (`eslint: key-spacing`).
  ```javascript
  // Bad
  const obj1 = { name : 'John' }
  const obj2 = { name:'John' }

  // Good
  const obj = { name: 'John' }
  ```
- Avoid trailing spaces at the end of lines (`eslint: no-trailing-spaces`).
- Avoid multiple empty lines (`eslint: no-multiple-empty-lines`).

#### **[Back to top](#table-of-contents)**

## Props

- Omit the value of the prop when it is explicitly true (`eslint: react/jsx-boolean-value`).
  ```javascript
  // Not preferable
  <Example isActive={true} />

  // Good
  <Example isActive />
  ```
- Always include an `alt` prop on <img> tags (`eslint: jsx-a11y/alt-text`).

  ```javascript
  // Bad
  <img src="example.jpg" />

  // Good
  <img alt="example" src="example.jpg" />
  ```
- Do not use words `image`, `photo`, `picture` in alt string (`eslint: jsx-a11y/img-redundant-alt`).

  ```javascript
  // Bad
  <img alt="image of square" src="square.jpg" />

  // Good
  <img alt="green square" src="square.jpg" />
  ```
- Do not use `<button>` without `type` property or with wrong value of it (`eslint:react/button-has-type`)
  ```javascript
    //bad
    const Hello = <button>Hello</button>
    const Hello = <button type="foo">Hello</button>
    const Hello = <button type={foo}>Hello</button>

    //good
    const Hello = <button type="button">Hello</button>
    const Hello = <button type="submit">Hello</button>
    const Hello = <button type="reset">Hello</button>
    const Hello = <button type={condition ? "button" : "submit"}>Hello</button>
  ```
- Avoid using an array index as `key` prop, prefer a stable ID (`eslint: react/no-array-index-key`).

  ```javascript
  // Bad
  {todos.map((todo, index) =>
    <Todo
      {...todo}
      key={index}
    />
  )}

  // Good
  {todos.map((todo, index) =>
    <Todo
      {...todo}
      key={todo.id}
    />
  )}
  ```

#### **[Back to top](#table-of-contents)**

## Refs

- Always use ref callbacks (`eslint: react/no-string-refs`).
  
  ```javascript
  // Bad
  <Example ref="myRef" />

  // Good
  <Example ref={ref => { this.myRef = ref }} />
  ```

#### **[Back to top](#table-of-contents)**

## Parentheses

- Wrap JSX tags in parentheses when they span more than one line (`eslint: react/jsx-wrap-multilines`).

  ```javascript
  // Bad
  render() {
    return <Example description="long description" name="bar">
              <ExampleChild />
           </Example>
  }

  // Good
  render() {
    return (
      <Example description="long description" name="bar">
        <ExampleChild />
      </Example>
    )
  }

  // Good, when single line
  render() {
    return <Example description="long description" name="bar" />
  }
  ```

#### **[Back to top](#table-of-contents)**

## Tags

- Always self-close tags that have no children (`eslint: react/self-closing-comp`).

  ```javascript
  // bad
  <Example role="admin"></Example>

  // good
  <Example role="admin" />
  ```
- If your component has multiline properties, close its tag on a new line (`eslint: react/jsx-closing-bracket-location`).

  ```javascript
  // Bad
  <Example
    isActive
    role="admin"
    description="description text" />

  // Good
  <Example
    isActive
    role="admin"
    description="description text"
  />
  ```
- Always use `<a>` only for links (`eslint:jsx-a11y/anchor-is-valid`).

- Always enforce that `<a>` tag have content and that the content is accessible to screen readers. Accessible means that it is not hidden using the `aria-hidden` prop (`eslint:jsx-a11y/anchor-has-content`)
  ```javascript
    //bad
    <a />
    <a><TextWrapper aria-hidden /></a>

    //good
    <a>Anchor Content!</a>
    <a><TextWrapper /></a>
  ```

#### **[Back to top](#table-of-contents)**
## Components

* Always use functional component if your component is stateless (`eslint:react/prefer-stateless-function`)
  ```javascript
    //bad
    class StateLess extends React.Component{
      render(){
        return <div>I'am a stateLess component</div>
      }
    }

    //good
    const Stateless = (props) => {
      return <div>I'am a stateLess component</div>
    }
  ```

* Don't declare unused `state` in youre `component` (`eslint:react/no-unused-state`)
  ```javascript
    //bad
    class MyComponent extends React.Component {
      state = { foo: 0 };
      render() {
        return <SomeComponent />;
      }
    }
  ```


* Don't use `setState` in `componentDidMount` method of lifecycle (`eslint:react/no-did-mount-set-state`)
  ```javascript
    //bad
    class NonOptimized {

      componentDidMount() {
        setState({})
      }

      render() {
        return (
          <div>
            This Component is non optimized because it does rerendering after mounting
          </div>
        )
      }
    }
  ```

#### **[Back to top](#table-of-contents)**

## JSX

* This rule prevents characters that you may have meant as `JSX` escape characters from being accidentally injected as a text node in `JSX` statements. (`eslint:react/no-unescaped-entities`)

* Always declare `React` in file where you use `JSX` pragma (`eslint:react/react-in-jsx-scope`)
  ```javascript
  //bad
    const Hello = <div>Hello {this.props.name}</div>

  //good
  import React from 'react'

  const Hello = <div>Hello {this.props.name}</div>
  ```
 * Always use `onKeyUp`, `onKeyDown` or `onKeyPress` with using `onClick` event. Coding for the keyboard is important for users with physical disabilities who cannot use a mouse, AT compatibility, and screenreader users. (`eslint:jsx-a11y/click-events-have-key-events`)
#### **[Back to top](#table-of-contents)**
