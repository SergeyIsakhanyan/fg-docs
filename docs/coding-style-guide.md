# Coding Style Guide

## Table of Contents

 - [**Basic**](#basic)
 - [**Class component vs stateless / functional component**](#class-component-vs-functional-component)
 - [**Naming**](#naming)
 - [**Quotes**](#quotes)
 - [**Spacing**](#spacing)
 - [**Props**](#props)
 - [**Refs**](#refs)
 - [**Parentheses**](#parentheses)
 - [**Tags**](#tags)
 - [**Methods**](#methods)

&nbsp;
&nbsp;

## Basic

* Only include one React component per file (`eslint: react/no-multi-comp`).
* Always use JSX syntax.

&nbsp;
&nbsp;

## Class component vs functional component

* If you have internal state and/or refs, use `React.Component` or `React.PureComponent`.

  ```
  class Example extends React.Component {
    constructor(props) {
      super(props)
      this.state = { value }
    }
    // ...
    render() {
      const { value } = this.state

      return (
        <div>
          <p>{value}</p>
        </div>
      )
    }
  }
  ```

* If you don’t have state or refs, prefer functions.

  ```
  const Example = ({ value }) => {
    return (
      <div>
        <p>{value}</p>
      </div>
    )
  }
  ```

  or

  ```
  function Example({ value }) {
    return (
      <div>
        <p>{value}</p>
      </div> 
    )
  }
  ```

Anonymous functions can make it harder to locate the problem in an Error's call stack. 
Anyway, prefer to use named function only if the function name is nessecary. Arrow function has it's own pros:  
* communicates to reader that there is no `this`, no `arguments`.
* readable / looks better.
* performance (arrow function marginally faster).

#### **[Back to top](#table-of-contents)**

## Naming

* **Extensions:** 
  - Use `.jsx` extension for React components.
  - Use `.js` extension for files which not containing `JSX` (utils, redux's actions/reducers).
  - Use `.less` extension for style files.
* **Filename:**
  - Use `PascalCase` for React components.
  - Use `camelCase` for React components' instance.
  - Use `lowercase` for redux's folders names, actions, reducers.
  - Use `snake_case` for core's folders names.
  - Use `lowercase` for style files' names.
* **Component Name:**
  - Use the filename or folder name as the component name.
  - Use `index.jsx` for the root component of a directory/folder.
    ```
    Example.jsx    --------------> export Example class/function
    Example folder -> index.jsx -> export Example class/function
    ```

  - Use `cascalCase` for Higher-order components and add `HOC` in the end.
  - Use `PamelCase` for wrapper components and add `Wrapper` in the end
    ```
    exampleFunctionalityHOC.js
    EventWrapper.jsx
    ```
  - If component is reusable, then it's name should describe component itself and not where it's used.

    ```
    // Bad
    export ProfileUsernameField ...
    export ProductInfoTextArea ...
    export SubmitButton ...

    // Good
    export InputField
    export TextAreaField
    export Button
    ```
  - Acronyms and initialisms should always be all uppercased.
    ```
    // Bad
    import SmsContainer from './SmsContainer'

    // Good
    import SMSContainer from './SMSContainer'
    ```

* **Props Naming:**
  - Avoid using DOM component prop names for React components.
    ```
    // Bad
    <Example className="exampleClass" />

    // Good
    <Example containerClass="exampleClass" />

    // Good
    <Example classNames={{ container: 'exampleClass' }} />
    ```

  - Props should be named to describe the componet itself. Props describe what a component does, not why it does.
    ```
    // Bad
    <Example hasSubmitPermission={true} />

    // Good
    <Example hasSubmitButton={true} />

    // Good
    <Example showSubmitButton={true} /> // less preferable
    ```

  - Prop name depending on type:
    |         |                                                                                  |
    | ------- | -------------------------------------------------------------------------------- |
    | Array   | – use plural nouns (items, countries, companies, events)                         |
    | Object  | – use noun (item, country, company, event)                                       |
    | Node    | – use prefix `node`(conatinerNode)                                               |
    | Element | – use prefix `element` (hoverElement)                                            |
    | Number  | – use prefix `num` or postfix `count` , `index` (numItems, itemCount, itemIndex) |
    | Boolean | – use prefix `is`, `can`, `has` (isVisible, canExpand, hasHeader)                |

* **Variable Naming:**
  - Always use `let` or `const` to declare variable (`eslint: no-undef, prefer-const`).
  - Use one `const` or `let` declaration per variable or assignment.
    ```
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

    ```
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

    ```
    // Bad
    let a = b = c = 1

    // Good
    let a = 1
    let b = a // let b = 1
    let c = a // let c = 1 or let c = b
    ```
  - Don't declare unused variables (`eslint: no-unused-vars`).
  - Avoid using single letter variables in functions.
    ```
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
  - Constant valiable should be uppercase only if it is exported.
    ```
    // Bad
    const PRIVATE_VARIABLE = 'used only in that file'

    // Bad, unnecessarily uppercase KEY
    export const OBJECT = {
      KEY: 'value'
    }

    // Not preferable
    export const apiKey = 'SOMEKEY'

    // Good
    export const API_KEY = 'SOMEKEY'

    export const OBJECT = {
      key: 'value'
    }
    ```

* **Function Naming:**
  - Avoid using single letter names.

    ```
    // Bad
    function q() {
      // ...
    }

    const a = () => { 
      // ,,,
    }

    // Good
    function query() {
      // ...
    }
    ```
  - Do not use trailing or leading underscores (`eslint: no-underscore-dangle`).
    ```
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
  - Don’t save references to `this`. Use arrow functions.
    ```
    // Bad
    function example () {
      const self = this // const that = this
      return function () {
        console.log(this)
      }
    }

    // Good
    function example () {
      return () => {
        console.log(this)
      }
    }
    ```

#### **[Back to top](#table-of-contents)**

## Quotes

* **Strings:** 
  - Use single quotes for strings.
    ```
    // Bad
    const name = "John"
    const name = `John`

    // Good
    const name = 'John'
    ```

  - Use double quotes for string props.
    ```
    // Bad
    <Example name='John' />
    <Example name={'John'} />
    <Example name={`John`} />

    // Good
    <Example name="John" />

    // Good
    const firstName = 'John'

    <Example name={firstName} />
    ```

  - Long strings should not be written across multiple lines using string concatenation. (Broken strings make code less searchable.)
    ```
    // Bad
    const errorMessage = 'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.'

    // Good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  - Use template strings instead of concatenation.
    ```
    const name = 'John'

    // Bad
    const concatMessage = 'How are you, ' + name + '?'
    const joinMessage = ['How are you, ', name, '?'].join()

    // Good
    const message = `How are you, ${name}?`
    ```

  - Never use eval() on a string (`eslint: no-eval`).

* **Styles:** 
  - Use single quotes for inline styles.

    ```
    // Bad
    <Example style={{ margin: "auto" }} />

    // Good
    <Example style={{ margin: 'auto' }} />
    ```
* **Objects:** 
  - Only quote properties that are invalid identifiers.

    ```
    // Bad
    const example = {
      'firstName': 'John',
      'lastName': 'Lennon',
      'e-mail': 'johnlennon@beatles.com'
    }

    // Good
    const example = {
      firstName: 'John',
      lastName: 'Lennon',
      'e-mail': 'johnlennon@beatles.com'
    }
    ```

#### **[Back to top](#table-of-contents)**

## Spacing

- Always include a single space in your self-closing tag (`eslint: no-multi-spaces, react/jsx-tag-spacing`).

  ```
  // Bad
  <Example   />

  // Bad
  <Example 
   />

  // Good
  <Example />
  ```
- Do not pad JSX curly braces with spaces (`eslint: react/jsx-curly-spacing`).

  ```
  // Bad
  <Example name={ name } />

  // Good
  <Example name={name} />
  ```

- Spacing in a function signature (`eslint: space-before-function-paren, space-before-blocks`).
  ```
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
  ```
  // Bad
  getFullName ()

  // Bad
  getFullName
  ()

  // Good
  getFullName()
  ```

- Spacing in generators (`eslint: generator-star-spacing`).
  ```
  // Bad
  function * exampleOne() {}
  const exampleTwo = function * () {}

  // Good
  function* exampleOne() {}
  const exampleTwo = function* () {}
  ```
- Spacing in arrays (`eslint: array-bracket-spacing`).
  ```
  // Bad
  const numbersArr = [ 1, 2, 3 ]
  const firstNum = numbersArr[ 0 ]

  // Good
  const numbersArr = [1, 2, 3]
  const firstNum = numbersArr[0]
  ```
- Spacing in objects (`eslint: object-curly-spacing`).
  ```
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
  ```
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

- Always use `camelCase` for prop names, or `PascalCase` if the prop value is a React component.

  ```
  // Bad
  <Example
    FirstName="John"
    phone_number={1234}
  />

  // Good
  <Example
    firstName="John"
    phoneNumber={1234}
  />
  ```
- Omit the value of the prop when it is explicitly true (`eslint: react/jsx-boolean-value`).
  ```
  // Not preferable
  <Example isActive={true} />

  // Good
  <Example isActive />
  ```
- Always include an `alt` prop on <img> tags (`jsx-a11y/alt-text`).

  ```
  // Bad
  <img src="example.jpg" />

  // Good
  <img alt="example" src="example.jpg" />
  ```
- Do not use words `image`, `photo`, `picture` in alt string (`eslint: jsx-a11y/img-redundant-alt`).

  ```
  // Bad
  <img alt="image of square" src="square.jpg" />

  // Good
  <img alt="green square" src="square.jpg" />
  ```
- Avoid using an array index as `key` prop, prefer a stable ID (`eslint: react/no-array-index-key`).

  ```
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
  
  ```
  // Bad
  <Example ref="myRef" />

  // Good
  <Example ref={ref => { this.myRef = ref }} />
  ```

#### **[Back to top](#table-of-contents)**

## Parentheses

- Wrap JSX tags in parentheses when they span more than one line (`eslint: react/jsx-wrap-multilines`).

  ```
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

  ```
  // bad
  <Example role="admin"></Example>

  // good
  <Example role="admin" />
  ```
- If your component has multiline properties, close its tag on a new line (`eslint: react/jsx-closing-bracket-location`).

  ```
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

#### **[Back to top](#table-of-contents)**

## Methods

- Do not `bind` event handlers in render method. Instead use arrow-functions or `bind` event handlers in the constructor.

  ```
  // Bad
  class extends React.Component {
    onClick() {
      // ...
    }

    render() {
      return <div onClick={this.onClick.bind(this)} />
    }
  }

  // Bad - may couse performance issues, creates new function on every render
  class extends React.Component {
    onClick = () => {
      // ...
    }

    render() {
      return <div onClick={this.onClick} />
    }
  }

  // Good
  class extends React.Component {
    constructor(props) {
      super(props);

      this.onClick = this.onClick.bind(this);
    }

    onClick() {
      // ...
    }

    render() {
      return <div onClick={this.onClick} />
    }
  }

  // Good
  class extends React.Component {
    onClick() {
      // ...
    }

    render() {
      return <div onClick={() => this.onClick()} />
    }
  }
  ```
- Do not use underscore prefix for internal methods of a React component.

  ```
  // Bad
  class extends React.Component {
    _onClick() {
      // ...
    }
    ...
  }

  // Good
  class extends React.Component {
    onClick() {
      // ...
    }
    ...
  }  
  ```

#### **[Back to top](#table-of-contents)**
