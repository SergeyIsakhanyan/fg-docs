# React Hook Rules Guide (ESLINT configurable)

## Table of Contnents


- **EsLint** configurable
     - [**Hooks Usage Rules**](#hooks-usage-rules)
     - [**Custom Hooks Rules**](#custom-hooks-rules)

&nbsp;
&nbsp;

## Hooks Usage Rules

* ### Only Call Hooks at the Top Level

    **Don't call Hooks inside loops, conditions, or nested functions.** Instead, always use Hooks at the top level of your React function, before any early returns.
    ```javascript
    // bad
    if (name !== '') {
        useEffect(function persistForm() {
            localStorage.setItem('formData', name);
        });
    }

    // bad
    for(let i = 0; i < 10; i++) {
        inputs[i] = useState('name' + i);
    }

    // bad
    function Bad1() {
        function handleClick() {
            const theme = useContext(ThemeContext);
        }
    }

    // good
    useEffect(function persistForm() {
        if (name !== '') {
            localStorage.setItem('formData', name);
        }
    });

    ```

* ### Only Call Hooks from React Functions

    **Don't call Hooks from React Class Components, only from React Function Components or Custom Hooks**
    ```javascript
    //bad
    class Bad extends React.Component {
        render() {
            useEffect( () => {} )
        }
    }

    //good
    function good(props){
        useEffect( () => {} )
        return(
            <>Good Example</>
        )
    }
    ```
* ### ESLint Configuration
    ESLint plugin called (`eslint-plugin-react-hooks`) that enforces these two rules.
    This plugin is included by default in (`Create React App.`)
    * Installation
    ```
    npm install eslint-plugin-react-hooks --save-dev
    ```
    * ESLint Configuration
    ```json
    {
        "plugins": [
            "react-hooks"
        ],
        "rules": {
            "react-hooks/rules-of-hooks": "error", 
            // Checks rules of Hooks
            "react-hooks/exhaustive-deps": "warn" 
            // Checks effect dependencies
        }
    }
    ```

&nbsp;
&nbsp;

## Custom Hooks Rules

* ### Use names only with starting `use`
    **A custom Hook is a JavaScript function whose name starts with "use" and that may call other Hooks.**
&nbsp;

    ```javascript
    //bad
    function myBadFriendStatus(friendID) {
        const [isOnline, setIsOnline] = useState(null);
        return isOnline;
    }

    //good
    function useFriendStatus(friendID) {
        const [isOnline, setIsOnline] = useState(null);
        return isOnline;
    }
    ```

