The **`useRef`** hook is a built-in React hook that allows you to **persist values** across renders without causing re-renders. It is primarily used to **reference DOM elements** directly, but can also be used to store any mutable value that doesn’t trigger a re-render when it changes.

In simpler terms, `useRef` helps you to **keep a reference** to an element or value that **does not change the UI** when it gets updated, unlike **`useState`** which triggers a re-render when the state changes.

### **Primary Use Cases of `useRef`**
1. **Accessing DOM Elements**: You can use `useRef` to get a reference to a DOM element (e.g., input fields, buttons, divs) and interact with it directly (e.g., focusing an input, reading values).
2. **Storing Mutable Values**: You can store data that doesn’t need to trigger a re-render (such as timers, previous state, or values that should persist between renders) without causing unnecessary updates to the component.

### **How `useRef` Works**

- **Syntax**:
    
    ```javascript
    const myRef = useRef(initialValue);
    ```
    
- **Parameters**:
    - `initialValue`: This is the initial value of the `ref`. It can be anything you want to store (a DOM element, a mutable variable, etc.).
    - The `myRef` object returned by `useRef` has a property `current` that holds the current value of the reference.

### **1. Accessing DOM Elements with `useRef`**
In many cases, you'll want to directly interact with a DOM element, such as focusing an input field when a button is clicked. `useRef` allows you to create a reference to the DOM element and access it when needed.

#### **Example: Focusing an Input Field**
```javascript
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null); // Create a ref for the input element

  const handleClick = () => {
    inputRef.current.focus(); // Focus the input when the button is clicked
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Focus me!" />
      <button onClick={handleClick}>Focus the input</button>
    </div>
  );
}

export default FocusInput;
```

In this example:
- **`inputRef`** is created using `useRef(null)`. The reference is attached to the input element via the `ref` attribute.
- When the **"Focus the input"** button is clicked, the `handleClick` function calls `inputRef.current.focus()` to focus the input field.

**Key Points**:
- `inputRef.current` holds the actual DOM element, and using `current`, you can manipulate or interact with the element directly (e.g., calling methods like `focus()`, `scrollIntoView()`, etc.).

### **2. Storing Mutable Values with `useRef`**
While `useState` can be used to store values that trigger re-renders when they change, `useRef` can be used to store values that do not trigger re-renders. This is useful for storing data that persists between renders but doesn’t need to cause the component to re-render every time it changes.

#### **Example: Storing Previous State Value**
If you need to store a previous state value for comparison without causing a re-render, you can use `useRef`.

```javascript
import React, { useState, useEffect, useRef } from 'react';

function PreviousCount() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();

  // Update the ref on each render
  useEffect(() => {
    prevCountRef.current = count;
  }, [count]);

  return (
    <div>
      <p>Current Count: {count}</p>
      <p>Previous Count: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default PreviousCount;
```

In this example:
- The `prevCountRef` is used to store the previous count value. It is updated inside the `useEffect` hook whenever the `count` value changes.
- `prevCountRef.current` holds the previous count, but changes to `prevCountRef` do **not trigger re-renders**.
- This is useful for situations where you need to compare the current state with the previous state without causing unnecessary re-renders.

### **3. Persisting Values Between Renders**
`useRef` can be used to persist values across re-renders without causing the component to re-render when the value changes. This is useful for things like timers or storing intermediate values.

#### **Example: Storing Timer ID**
```javascript
import React, { useEffect, useRef } from 'react';

function Timer() {
  const timerRef = useRef(null);

  useEffect(() => {
    timerRef.current = setInterval(() => {
      console.log('Timer is running...');
    }, 1000);

    // Cleanup on component unmount
    return () => {
      clearInterval(timerRef.current);
    };
  }, []);

  return <p>Timer is running every second. Check the console.</p>;
}

export default Timer;
```

In this example:
- The `timerRef` is used to store the timer ID created by `setInterval()`.
- `clearInterval(timerRef.current)` ensures that the timer is cleared when the component unmounts, preventing memory leaks.

Since `useRef` persists values across renders, the timer ID doesn’t need to be part of the state, which would otherwise cause unnecessary re-renders.

### **Key Differences Between `useRef` and `useState`**
1. **Re-renders**:
    - **`useRef`** does not trigger a re-render when its value changes. It is ideal for storing values that don’t need to cause the component to re-render, like DOM references or timers.
    - **`useState`** triggers a re-render whenever its value is updated, making it suitable for state that directly affects the UI.
        
2. **Value Persistence**:
    - Both **`useRef`** and **`useState`** persist values across renders, but **`useState`** causes re-renders when the value changes, while **`useRef`** doesn’t.
        
3. **Use Case**:
    - **`useRef`** is best for keeping references to DOM elements, mutable values, or objects that don’t require re-renders.
    - **`useState`** is best for values that should trigger re-renders when they change and are part of the component’s state (e.g., form input values, count, etc.).

### **When to Use `useRef`**
- **Accessing DOM elements**: For focusing input fields, scrolling to an element, or triggering animations.    
- **Storing mutable data**: For things like tracking the previous value of a state, keeping track of a timer ID, or storing data that needs to persist but doesn’t affect the UI.
- **Avoiding re-renders**: When you need to store data that shouldn’t trigger re-renders, like setting up event listeners, managing non-UI-related data, or keeping references to third-party libraries.

## Resource
- [React Reference - useRef](https://react.dev/reference/react/useRef)