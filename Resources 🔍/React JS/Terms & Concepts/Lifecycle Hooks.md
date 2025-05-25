**Lifecycle hooks** are methods or functions provided by frameworks like **React**, **Vue**, and **Angular** that allow you to run specific code at certain points during the lifecycle of a component or application. These hooks are especially useful for managing resources, fetching data, or cleaning up resources when components are created, updated, or destroyed.

Lifecycle hooks are **triggered automatically** by the framework at certain stages, and they enable you to **interact with the component's lifecycle**. For example, in React, lifecycle hooks allow you to perform actions when a component is created, updated, or removed.

### Lifecycle Hooks in React:

In **React**, lifecycle hooks are available primarily for **class components** and **functional components** (via **React hooks**). React provides various hooks that correspond to different stages in a component’s lifecycle.

#### 1. **Class Component Lifecycle Hooks**:

Class components in React have built-in lifecycle methods. These methods are divided into three main phases: **Mounting**, **Updating**, and **Unmounting**.

##### a. **Mounting**:

The mounting phase refers to the process when a component is created and inserted into the DOM.

- **`constructor()`**:
    
    - This method is called when the component is being created. It is used to initialize state, bind methods, or do any other setup.
        
    
    ```javascript
    constructor(props) {
      super(props);
      this.state = { count: 0 };
    }
    ```
    
- **`componentDidMount()`**:
    
    - This method is called once the component is mounted to the DOM. It is typically used for **fetching data** or performing any other setup that requires the component to be rendered first.
        
    
    ```javascript
    componentDidMount() {
      console.log('Component has been mounted');
    }
    ```
    

##### b. **Updating**:

The updating phase occurs when the component’s **state** or **props** change, causing a re-render.

- **`shouldComponentUpdate(nextProps, nextState)`**:
    
    - This method is called before the component re-renders. It allows you to decide whether the component should update (return `true`) or not (return `false`).
        
    
    ```javascript
    shouldComponentUpdate(nextProps, nextState) {
      return nextState.count !== this.state.count;
    }
    ```
    
- **`componentDidUpdate(prevProps, prevState)`**:
    
    - This method is called after the component has re-rendered. It can be used to perform side effects like network requests or manually updating the DOM.
        
    
    ```javascript
    componentDidUpdate(prevProps, prevState) {
      if (prevState.count !== this.state.count) {
        console.log('State has changed');
      }
    }
    ```
    

##### c. **Unmounting**:

The unmounting phase occurs when a component is removed from the DOM.

- **`componentWillUnmount()`**:
    
    - This method is called before the component is removed from the DOM. It is typically used for cleanup tasks such as **clearing timers**, **canceling network requests**, or **unsubscribing from events**.
        
    
    ```javascript
    componentWillUnmount() {
      console.log('Component will unmount');
    }
    ```
    

#### Example of a Class Component with Lifecycle Hooks:

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log('Component has mounted');
  }

  shouldComponentUpdate(nextProps, nextState) {
    return nextState.count !== this.state.count;
  }

  componentDidUpdate() {
    console.log('Component did update');
  }

  componentWillUnmount() {
    console.log('Component will unmount');
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

---

### 2. **Functional Component Lifecycle Hooks (React Hooks)**:

With the introduction of **React hooks** (starting from React 16.8), functional components were given the ability to manage lifecycle events using hooks. The most commonly used hook for lifecycle management in functional components is the **`useEffect`** hook.

##### a. **`useEffect` Hook**:

The `useEffect` hook serves as a replacement for many class component lifecycle methods. It can be used for running side effects in functional components, such as data fetching, subscriptions, or manually manipulating the DOM.

- **`useEffect` as `componentDidMount`** (Run once after the first render):
    
    ```javascript
    useEffect(() => {
      console.log('Component mounted');
    }, []); // Empty dependency array means it runs once
    ```
    
- **`useEffect` as `componentDidUpdate`** (Run every time the component updates):
    
    ```javascript
    useEffect(() => {
      console.log('Component updated');
    }, [count]); // Dependency array ensures it runs when 'count' changes
    ```
    
- **`useEffect` as `componentWillUnmount`** (Cleanup before component is removed):
    
    ```javascript
    useEffect(() => {
      return () => {
        console.log('Component will unmount');
      };
    }, []); // Cleanup on unmount
    ```
    

##### Example of a Functional Component Using `useEffect`:

```javascript
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('Component mounted');
    return () => {
      console.log('Component will unmount');
    };
  }, []); // Runs only once after mount and once before unmount

  useEffect(() => {
    console.log('Component updated');
  }, [count]); // Runs every time 'count' changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

In this example:

- The **first `useEffect`** runs only once when the component mounts and performs cleanup when the component unmounts.
    
- The **second `useEffect`** runs whenever the `count` state changes, which is similar to `componentDidUpdate`.
    

---

### React Lifecycle Phases Summary:

|**Phase**|**Class Component Lifecycle Methods**|**Functional Component (useEffect) Equivalent**|
|---|---|---|
|**Mounting**|`constructor()`, `componentDidMount()`|`useEffect(() => {}, [])` (empty dependency array)|
|**Updating**|`shouldComponentUpdate()`, `componentDidUpdate()`|`useEffect(() => {}, [dependencies])` (runs on dependency change)|
|**Unmounting**|`componentWillUnmount()`|`useEffect(() => { return () => {} }, [])` (cleanup on unmount)|

---

### Conclusion:

**Lifecycle hooks** are essential for managing side effects, performing actions at specific points in a component’s lifecycle, and ensuring your app runs smoothly. In **class components**, React provides methods like `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnmount()`. For **functional components**, React introduced **hooks**, such as `useEffect`, which provides a flexible way to handle lifecycle events in a declarative manner. Understanding how and when to use these hooks allows you to create more dynamic, responsive, and maintainable React applications.

## Resource
- [W3Schools React - Lifecycle](https://www.w3schools.com/react/react_lifecycle.asp)