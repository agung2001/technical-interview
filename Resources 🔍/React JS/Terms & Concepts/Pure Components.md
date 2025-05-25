In **React**, a **Pure Component** is a component that **only re-renders** when its **props** or **state** change. Pure components are a type of **optimization** to improve performance, as they implement **shallow comparison** between the current and next props and state to determine if the component needs to be re-rendered.

### Key Features of Pure Components:

1. **Shallow Comparison**:
    
    - A **pure component** performs a **shallow comparison** of the **current props** and **state** with the **next props** and **state**. If neither the props nor the state has changed, the component **does not re-render**. This helps improve performance by preventing unnecessary re-renders.
        
    - A shallow comparison checks whether:
        
        - Primitive values (like strings, numbers, booleans) are the same.
            
        - References to objects or arrays are the same, meaning it only checks whether the reference has changed, not the internal structure.
            
    
    **Example**:
    
    ```javascript
    const obj = { a: 1 };
    const arr = [1, 2, 3];
    const prevObj = obj;
    const prevArr = arr;
    
    // Shallow comparison will return false because references to obj and arr are different
    ```
    
2. **Performance Optimization**:
    
    - Pure components help optimize performance by avoiding unnecessary **re-renders**. This is particularly useful in complex or large applications, where re-rendering components can become costly in terms of performance.
        
3. **React's `PureComponent`**:
    
    - React provides a built-in class `PureComponent` that automatically implements `shouldComponentUpdate` with a shallow comparison for **props** and **state**. If the props or state haven't changed, it prevents the re-render of the component.
        
4. **React.memo for Functional Components**:
    
    - For **functional components**, React offers a **higher-order component** called `React.memo`. It provides similar behavior to `PureComponent`, performing a shallow comparison of props to decide whether to re-render the component.
        
    
    **Example of a PureComponent using React.memo**:
    
    ```javascript
    const MyComponent = React.memo((props) => {
      return <div>{props.name}</div>;
    });
    
    // This component will only re-render if the 'name' prop changes
    ```
    

---

### Example of `PureComponent`:

Here’s an example of a **class-based Pure Component** using `React.PureComponent`:

```javascript
import React from 'react';

class MyComponent extends React.PureComponent {
  render() {
    console.log('Rendering MyComponent');
    return <div>{this.props.name}</div>;
  }
}

export default MyComponent;
```

In this example, `MyComponent` is a **pure component** because it extends `React.PureComponent`. It will **only re-render** if the `name` prop changes. If the `name` prop stays the same, React will **skip the re-render**, which can improve performance.

---

### `React.memo` for Functional Components:

In modern React development, **functional components** are widely used, and `React.memo` is the functional equivalent of `PureComponent`.

```javascript
import React from 'react';

const MyComponent = React.memo(({ name }) => {
  console.log('Rendering MyComponent');
  return <div>{name}</div>;
});

export default MyComponent;
```

- `React.memo` ensures that the component is only re-rendered when the **props** change. It performs a **shallow comparison** of the previous and next props to determine whether a re-render is necessary.
    

---

### When to Use Pure Components:

1. **Static or Unchanging Props/State**:
    
    - Pure components are most beneficial when your component receives **static props** or **props that don't change often**. For example, a component that displays static content or represents a UI element that does not change frequently would benefit from being a pure component.
        
2. **Optimization for Large Applications**:
    
    - In large applications with many components, using pure components can help avoid unnecessary re-renders, which can improve overall performance.
        
3. **Avoiding Complex Logic for `shouldComponentUpdate`**:
    
    - If you need a custom `shouldComponentUpdate` logic that involves **shallow prop comparison**, using `PureComponent` (or `React.memo` for functional components) is a good alternative as it automates this logic for you.
        

---

### Limitations of Pure Components:

1. **Shallow Comparison**:
    
    - **Pure components** use **shallow comparison** for props and state, which means they only check if the references to objects or arrays have changed. If the **content** of an object or array changes but its reference remains the same, the component won't re-render, which could lead to stale UI.
        
    - **Example**:
        
        ```javascript
        const prevObj = { a: 1 };
        const nextObj = { a: 1 }; // Same content, different reference
        
        // PureComponent won't re-render because the references are different
        ```
        
2. **Performance Hit with Large or Complex Objects**:
    
    - If your props or state include large or deeply nested objects, shallow comparison can be inefficient because it only checks references at the first level. Deep changes within nested objects will not trigger re-renders unless the reference itself changes.
        
3. **Not Always Needed**:
    
    - Not all components benefit from being pure. If a component’s props change frequently or if the component is simple, using pure components may introduce unnecessary overhead. In these cases, traditional components or memoization techniques may be sufficient.
        

---

### Conclusion:

A **Pure Component** in React is a component that **optimizes performance** by ensuring it only re-renders when its **props or state** change. It relies on **shallow comparison** to determine if a re-render is necessary, making it useful for optimizing performance in larger applications or with components that don’t frequently change their state.

- **Class-based components** can use `React.PureComponent`.
    
- **Functional components** can use `React.memo`.
    

While pure components can improve performance, developers should be cautious about their use, especially with complex or nested objects where shallow comparison might not be sufficient.