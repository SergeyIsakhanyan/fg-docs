# Coding Style Guide

## Table of Contents
 - [**Class component vs stateless / functional component**](#class-component-vs-functional-component)
 - [**Naming**](#naming)
 - [**Quotes**](#quotes)
 - [**Props**](#props)
 - [**Methods**](#methods)

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
  - Use `lowercase` for folders names, actions, reducers, style files' names.
* **Component Name:**
  - Use the filename or folder name as the component name.
  - Use `index.jsx` for the root component of a directory/folder.
    ```
    Example.jsx    --------------> export Example class/function
    Example folder -> index.jsx -> export Example class/function
    ```

  - Use `PascalCase` for Higher-order components and add `HOC` in the end.
  - Use `camelCase` for wrapper components and add `Wrapper` in the end
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

  // Good
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
