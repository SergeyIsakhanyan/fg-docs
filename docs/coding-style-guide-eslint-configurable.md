
# Coding Style Guide (ESLINT configurable)

## Table of Contents

 - **ESLint** configurable
   - [**Basic**](#basic)
   - [**Naming**](#naming)
   - [**Quotes**](#quotes)
   - [**Spacing**](#spacing)
   - [**Props**](#props)
   - [**Refs**](#refs)
   - [**Parentheses**](#parentheses)
   - [**Tags**](#tags)

&nbsp;
&nbsp;

## Basic

* Only include one React component per file (`eslint: react/no-multi-comp`).
* Always use JSX syntax (`eslint: react/jsx-filename-extension`).

&nbsp;
&nbsp;

#### **[Back to top](#table-of-contents)**

## Naming

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
* **Function Naming:**
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
    #### **[Back to top](#table-of-contents)**
    
    ## Quotes
* **Strings:** 
- Never use eval() on a string (`eslint: no-eval`).

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

- Omit the value of the prop when it is explicitly true (`eslint: react/jsx-boolean-value`).
  ```
  // Not preferable
  <Example isActive={true} />

  // Good
  <Example isActive />
  ```
- Always include an `alt` prop on <img> tags (`eslint: jsx-a11y/alt-text`).

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
