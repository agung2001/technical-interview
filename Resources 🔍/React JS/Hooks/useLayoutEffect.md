```ad-warning
`useLayoutEffect` can hurt performance. Prefer [`useEffect`](https://react.dev/reference/react/useEffect) when possible.
```

The **`useLayoutEffect`** hook is one of the React hooks that is used to perform **side effects** in function components. It is very similar to the **`useEffect`** hook, but with one key difference: **`useLayoutEffect`** runs **synchronously** after all DOM mutations but **before the browser has painted** the updated UI to the screen.

This makes **`useLayoutEffect`** useful for scenarios where you need to **measure the DOM** (e.g., getting the dimensions of an element) or make adjustments that may affect layout, and you want to ensure those changes are applied **before** the page is rendered visually.

### **`useLayoutEffect` vs. `useEffect`**

- **`useEffect`**: Runs asynchronously after the render cycle. It’s designed for side effects that don’t require immediate layout changes, such as data fetching, setting up subscriptions, or interacting with external APIs.
- **`useLayoutEffect`**: Runs synchronously **after** the DOM has been updated but **before** the browser paints the changes. This ensures any updates to the DOM (e.g., layout adjustments or measurements) are applied immediately before the user sees the update.

### **When to Use `useLayoutEffect`**
You should use `useLayoutEffect` when you need to perform actions that:
- **Require DOM measurements** (e.g., measuring an element’s size, position, or scroll position).
- **Modify the layout** in ways that need to happen before the page is painted, such as changing the width/height of elements or adjusting scroll positions.

**Examples** include:
- Synchronously measuring the size or position of DOM elements.
- Performing animations that depend on the layout (like positioning elements absolutely).
- Preventing flicker by ensuring the DOM is updated before the user sees any change.

### **Syntax of `useLayoutEffect`**

```javascript
useLayoutEffect(() => {
  // Code to perform side effects
  return () => {
    // Cleanup (optional)
  };
}, [dependencies]);
```

- **Effect Function**: The function passed to `useLayoutEffect` runs after the DOM is updated but before the browser paints. This is where you can perform your measurements or DOM manipulations.
- **Cleanup Function**: Optionally, you can return a cleanup function from `useLayoutEffect` (just like `useEffect`). This will run when the component unmounts or when the effect dependencies change.
- **`dependencies` Array**: Just like `useEffect`, you can pass an array of dependencies. The effect will only run when one of these dependencies has changed.

### **Example of `useLayoutEffect`**

Let’s look at an example where `useLayoutEffect` is used to measure the size of an element and adjust its position or layout accordingly.

```javascript
import React, { useState, useLayoutEffect, useRef } from 'react';

function Component() {
  const [width, setWidth] = useState(0);
  const divRef = useRef(null); // Ref to the DOM element we want to measure

  // Use useLayoutEffect to measure the width before the browser paints
  useLayoutEffect(() => {
    // Get the width of the element after the DOM has been updated
    if (divRef.current) {
      setWidth(divRef.current.offsetWidth); // Set width state
    }
  }, []); // Empty dependency array ensures it runs only once after the initial render

  return (
    <div>
      <div ref={divRef} style={{ padding: '20px', border: '1px solid black' }}>
        This is a div.
      </div>
      <p>The width of the div is: {width}px</p>
    </div>
  );
}

export default Component;
```

#### **Explanation**:
- **`divRef`** is used to reference the DOM element (the `<div>`).
- **`useLayoutEffect`** is used to measure the width of the div after the DOM updates but before the browser renders the changes on screen.
- The width of the element is saved in the `width` state and displayed in the component.

By using **`useLayoutEffect`**, the width of the element is measured **before** the browser paints the updated UI, ensuring that the layout is correct and prevents visual flicker or incorrect sizing on initial render.

### **When Not to Use `useLayoutEffect`**
- **Performance Concerns**: Since **`useLayoutEffect`** runs synchronously before the browser paints, it can block the browser from rendering if the effect takes too long. This can cause performance issues, especially on slower devices or with heavy computations. Use `useEffect` unless you specifically need to interact with the DOM synchronously.
- **When DOM Manipulation Isn’t Needed Immediately**: If you don’t need to perform DOM measurements or make layout changes right away, prefer using `useEffect` instead of `useLayoutEffect` to avoid blocking the rendering process.

### **Key Differences Between `useEffect` and `useLayoutEffect`**

|**Aspect**|**`useEffect`**|**`useLayoutEffect`**|
|---|---|---|
|**Timing**|Runs asynchronously after the DOM has been painted.|Runs synchronously after the DOM is updated but before the paint.|
|**Use Case**|For side effects like data fetching, subscriptions, etc.|For reading or modifying the DOM before the user sees any changes.|
|**Performance**|Non-blocking (does not block the browser from painting).|Can block rendering if the effect is heavy or slow, leading to performance issues.|
|**Common Scenarios**|Fetching data, setting up external subscriptions.|Measuring or modifying DOM layout, setting focus, or preventing layout flicker.|

## Resource
- [React Reference - useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)