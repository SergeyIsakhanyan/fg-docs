# IDE - Integrated development environment

- [IDE - Integrated development environment](#ide---integrated-development-environment)
  - [Visual Studio Code (VS Code)](#visual-studio-code-vs-code)
    - [Pros](#pros)
    - [Cons](#cons)
  - [WebStorm](#webstorm)
    - [Pros](#pros-1)
    - [Cons](#cons-1)
- [Linters](#linters)
  - [Static Analysis](#static-analysis)
  - [Code standardizing](#code-standardizing)
  - [Performance improvements](#performance-improvements)
- [ESLint](#eslint)

An integrated development environment (IDE) is a software application that provides comprehensive facilities to computer programmers for software development. An IDE normally consists of at least:

- `Source code editor`
- `Build automation tools (building executables)`
- `Debugger`

Some IDEs, such as `NetBeans` and `Eclipse`, contain the necessary `compiler`, `interpreter`, or both.

Basically, IDE is a piece of software with a wide range of functions that help in the development of other software.
Typically, an IDE includes the following features (here is the list of features that are more inherent in a Javascript IDE):

- `Autocomplete`
- `Text editor fields`
- `Syntax checking`
- `Syntax highlighter`
- `Provide a suggestion`
- `IDE should allow you to quickly go to the definition of class or method`
- `Shortcuts for ease of access`
- `Plugin support to extend functionality`
- `Auto importing`
- `Refactoring`
- `Dead code hints`

***NOTE:*** *there is no standard set of features an IDE should have.*

Here is the list of most popular IDE's for JavaScript:

- `Visual Studio Code`
- `Webstorm`
- `Atom`
- `Brackets`
- `Komodo IDE`
- `Sublime Text`
- `Eclipse`
- `Light Table`
- `Codelobster`

Now let's see how the most popular IDE's for JavaScript offer as mentioned features and we will try to understand which one is preferable.

## Visual Studio Code (VS Code)

### Pros
- **VS Code is mostly open-source and 100% free**
- **The design is very modern, slick, minimalistic and customizable**  
  It's very hard to talk about design, because UI can be changed by the user to create their own.
- **Performance**  
  VS Code's performance is very good untill adding a few heavy extensions. They can slow down VS Code and use more resources. Also we have to mention that VS Code backed by `Electron`, which is known as resource-hungry framework.
- **Extendable**  
  VS Code's extendability depends on extensions and plug-ins. Without any extension installed, all you get is pure UI, basic autocomplition, syntax highlighting, debugger and some Git management tools. This extendability mostly because of marketplace of 10K+ extensions and themes.
- **Easy to install and use extensions**
- **Advanced breakpoint**
- **Integrated terminal**
- **Autocomplete**
- **Debugging**

### Cons
- **Longer launch time compared to other editors**
- **Sometimes it can become very unresponsive and a little laggy**
- **Too many extensions may cause performance issues**
- **Some updates and can crash your system**

## WebStorm

### Pros
- **Performance**  
  Comparing to VS Code, WebStorm uses `JVM` under the hood, and that's makes WebStorm faster and more optimized than any `Elecetron` app.
- **Everything is built-in**  
  Pretty much all the popular JavaScript frameworks, tools, and libraries have their place in WebStorm. So developer don't need to do additional work on startup and they  can just install the software and start working.
- **Auto importing**  
  Auto importing works better in WebStorm than in VS Code. You can copy and paste some code from one file to another in WebStorm and WebStorm can automatically import any missing symbols that are not already imported in the file.
- **Autocomplete**
- **Refactoring**  
  WebStorm is better at refactoring JavaScript/TypeScript code.
- **Debugging**
- **Code style and best practices**  
  WebStorm gives you hints related to any duplicated code it finds in your project which could be a good indication that things should be refactored for better re-usability.
- **Dead code hints**  
  WebStorm will tell you if exported variables are not used anywhere in your project and can be safely deleted. VSCode can only tell you if a variable is not being used in the current file.
- **Integrated terminal**
- **Good Support**

### Cons
- **Paid**
- **Customization capabilities**  
  As we say, WebStorm has everything already built-in and that may cause beginners to feel overwhelmed by the number of all the buttons, menus. There is a slight level of customizability with different extensions for different features, but nothing near the size of the VS Code extension marketplace.
- **Intelligence feature only for JavaScript**

# Linters

According to Wikipedia, linter is a tool that analyzes source code to flag programming errors, bugs, stylistic errors, and suspicious constructs.

## Static Analysis
Static Analysis means that automated software runs through your code source without executing it. It statically checks for potential bugs, memory leaks, and any other check that may be useful.

## Code standardizing
Standardizing your code is a great way to move the conversation to a more productive level. Having a guideline and running linters against the codebase avoids aesthetical changes in your pull request, like replacing all tabs for spaces, indenting a variable assignment, or even line breaks after a given number of characters.

## Performance improvements
Many linters include a performance check. For example in CSS, the universal selector (*) may slow down a page loading time. Avoiding them is good practice.

# ESLint

Nowdays there are many linters for JavaScript, but now will talk about ESLint as it is the best linter.

- ESLint analyzes your code for style and coding errors that can lead to bugs.
- ESLint can format your code.
- ESLint will let you know what’s wrong with your code formatting and give you options to fix the issue.
- ESLint considers code quality rules (`no-unused-vars`, `no-implicit-globals`).
