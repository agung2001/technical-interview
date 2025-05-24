`useEffect` is a built-in hook in React, a JavaScript library for building user interfaces. It allows you to perform side effects in functional components, such as data fetching, DOM manipulation, or subscribing to external resources. Essentially, `useEffect` provides a way to handle lifecycle events in functional components.

The primary purpose of `useEffect` is to execute code that has side effects after the component renders, and potentially after subsequent updates. It ensures that these side effects are managed properly and don't cause unnecessary re-renders or memory leaks.

Here's how you use `useEffect`:

1. Import the hook:
   ```jsx
   import React, { useState, useEffect } from 'react';
   ```

2. Define a functional component and use the `useEffect` hook within it. Pass a function as the first argument to `useEffect`. This function will be executed after the component renders:
   ```jsx
   function ExampleComponent() {
     useEffect(() => {
       // This code runs after the component renders
       console.log('Component rendered');
     });
   }
   ```

3. The `useEffect` function can have a second argument, which is an array of dependencies. When provided, `useEffect` will only run if any of the dependencies change between renders. This helps optimize when and how often the effect runs:
   ```jsx
   function ExampleComponent() {
     const [count, setCount] = useState(0);

     useEffect(() => {
       console.log('Component rendered');
     }, [count]); // Run the effect only if 'count' changes
   }
   ```

4. In addition to cleanup, you can return a cleanup function from the `useEffect` function. This function will be executed when the component unmounts or before the effect runs again due to dependency changes:
   ```jsx
   function ExampleComponent() {
     useEffect(() => {
       console.log('Component rendered');
       
       return () => {
         console.log('Component unmounted or effect is re-running');
       };
     });
   }
   ```

`useEffect` is a powerful tool for managing side effects in React components while maintaining a clear and declarative code structure. It helps you keep your components focused on rendering and user interactions while abstracting away the complexities of managing external data or resources.

## Resource
- [React Referenc - useEffect](https://react.dev/reference/react/useEffect)