The **`useCallback`** hook is a built-in React hook that returns a **memoized** version of a callback function. It helps optimize performance by preventing unnecessary re-creations of functions on every render.

When you pass a function as a prop or use it within a child component, React creates a **new instance** of that function every time the component re-renders. This can be inefficient, especially when the function is passed down to child components that don’t need it to change on every render.

The `useCallback` hook allows you to **memoize** the function, meaning it will only be re-created if certain dependencies have changed, rather than on every render. This can help avoid unnecessary re-renders of child components or unnecessary recalculations of values in performance-critical parts of your app.

### **Why Use `useCallback`?**
- **Preventing Unnecessary Re-renders**: When you pass a function down to child components, that child will re-render every time the parent re-renders (even if the function itself hasn't changed). `useCallback` helps by ensuring that the same function instance is passed to the child unless specific dependencies change.
- **Performance Optimization**: Memoizing functions helps prevent the unnecessary recalculation of functions and prevents children from unnecessarily re-rendering when the function reference doesn't change. This can be especially useful in large applications with complex state or deep component trees.

### **Syntax of `useCallback`**

```javascript
const memoizedCallback = useCallback(
  () => {
    // Your function logic
  },
  [dependencies]  // Array of dependencies that will trigger the function to be re-created
);
```

- **`memoizedCallback`**: The memoized version of the callback function.
- **`[dependencies]`**: The array of dependencies that the callback function depends on. If any of these dependencies change, the function will be re-created; otherwise, the same instance will be used.

### **Example of `useCallback`**
Let’s go through an example to understand how `useCallback` works.

#### **Without `useCallback`**
In the following example, the `ParentComponent` re-renders every time the button is clicked, and a **new instance** of the `handleClick` function is created on each render:

```javascript
import React, { useState } from 'react';

function ChildComponent({ handleClick }) {
  console.log('Child re-rendered');
  return <button onClick={handleClick}>Click me</button>;
}

function ParentComponent() {
  const [count, setCount] = useState(0);

  // A new function is created every time the Parent component renders
  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <ChildComponent handleClick={handleClick} />
      <p>Count: {count}</p>
    </div>
  );
}

export default ParentComponent;
```

In this case:
- **`handleClick`** is a new function on every render.
- Since the `handleClick` function is passed as a prop to `ChildComponent`, it causes `ChildComponent` to re-render every time the parent (`ParentComponent`) re-renders.

#### **With `useCallback`**

To optimize this, you can use the `useCallback` hook to **memoize** the `handleClick` function so that it is only re-created when the `count` changes.

```javascript
import React, { useState, useCallback } from 'react';

function ChildComponent({ handleClick }) {
  console.log('Child re-rendered');
  return <button onClick={handleClick}>Click me</button>;
}

function ParentComponent() {
  const [count, setCount] = useState(0);

  // Memoize the function, so it is only recreated when `count` changes
  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);  // Only recreate handleClick if `count` changes

  return (
    <div>
      <ChildComponent handleClick={handleClick} />
      <p>Count: {count}</p>
    </div>
  );
}

export default ParentComponent;
```

In this example:
- **`useCallback`** ensures that the `handleClick` function is only recreated when the `count` state changes.
- If the `count` doesn’t change, React will **reuse the same function** and prevent unnecessary re-renders of `ChildComponent`.

### **When to Use `useCallback`**
- **Passing Functions as Props to Child Components**: If you're passing functions down to child components and those functions don’t depend on the component’s state or props, `useCallback` ensures the function reference remains stable across renders, preventing unnecessary re-renders of the child component.
- **Event Handlers in Lists**: When working with lists (especially large ones), `useCallback` can be used to memoize event handlers, preventing unnecessary re-renders for every item in the list.
- **Expensive Computations or Operations**: If a function performs expensive computations or operations and is called repeatedly (e.g., inside a loop or in response to frequent events), `useCallback` can help optimize its execution by memoizing it and reducing unnecessary recalculations.

### **Example: Optimizing Performance with `useCallback`**

Let’s say you have a large list of items, and each item has a delete button. Without `useCallback`, each button’s click handler would create a new function on each render, leading to unnecessary re-renders.

```javascript
import React, { useState } from 'react';

function ListItem({ item, onDelete }) {
  console.log('Item re-rendered:', item.id);
  return (
    <div>
      {item.name} <button onClick={() => onDelete(item.id)}>Delete</button>
    </div>
  );
}

function ItemList() {
  const [items, setItems] = useState([
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' },
  ]);

  const deleteItem = (id) => {
    setItems(items.filter(item => item.id !== id));
  };

  return (
    <div>
      {items.map((item) => (
        <ListItem key={item.id} item={item} onDelete={deleteItem} />
      ))}
    </div>
  );
}

export default ItemList;
```

In this example:

- Each time the `ItemList` component re-renders (for example, when an item is deleted), all `ListItem` components will re-render, and a **new function** (`onDelete`) will be created for each button.
    

Now, using **`useCallback`** to **memoize** the `deleteItem` function:

```javascript
import React, { useState, useCallback } from 'react';

function ListItem({ item, onDelete }) {
  console.log('Item re-rendered:', item.id);
  return (
    <div>
      {item.name} <button onClick={() => onDelete(item.id)}>Delete</button>
    </div>
  );
}

function ItemList() {
  const [items, setItems] = useState([
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' },
  ]);

  // Memoize the delete function to prevent unnecessary re-renders
  const deleteItem = useCallback((id) => {
    setItems(items.filter(item => item.id !== id));
  }, [items]);  // Recreate the function only if `items` changes

  return (
    <div>
      {items.map((item) => (
        <ListItem key={item.id} item={item} onDelete={deleteItem} />
      ))}
    </div>
  );
}

export default ItemList;
```

In this optimized version:

- **`useCallback`** ensures that the `deleteItem` function is not recreated on every render, thus avoiding unnecessary re-renders of the `ListItem` components.

### **Conclusion**

The **`useCallback`** hook is useful for **memoizing callback functions**, especially when those functions are passed as props to child components. By keeping the same function instance across renders, `useCallback` helps prevent unnecessary re-renders and improves performance in React applications.

However, it's important to use `useCallback` only when necessary because it adds overhead, and in some cases, it may not offer significant performance improvements. It's most beneficial when dealing with large lists, frequent re-renders, or when passing functions down to deeply nested components.

## Resource
- [React Reference - useCallback](https://react.dev/reference/react/useCallback)