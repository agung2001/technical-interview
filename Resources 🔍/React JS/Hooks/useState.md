`useState` is a built-in hook in React, a JavaScript library for building user interfaces. It is used to add state management capabilities to functional components. With `useState`, you can declare and manage state variables within a functional component, allowing you to update and track changes in the component's state over time.

Here's how `useState` works:

1. Import the hook:
   ```jsx
   import React, { useState } from 'react';
   ```

2. Use `useState` in a functional component to declare a state variable and its initial value. `useState` returns an array with two elements: the current state value and a function to update that value.
   ```jsx
   function ExampleComponent() {
     const [count, setCount] = useState(0);
     // 'count' is the state variable, and 'setCount' is the function to update it
   }
   ```

3. You can use the state variable (`count` in this case) in your component's JSX to display the current value:
   ```jsx
   return (
     <div>
       <p>Count: {count}</p>
     </div>
   );
   ```

4. To update the state, you use the provided state update function (`setCount` in this case):
   ```jsx
   <button onClick={() => setCount(count + 1)}>Increment</button>
   ```

By using `useState`, React handles the management of state for you, ensuring that when the state is updated, the component re-renders to reflect the changes. This makes it easy to create dynamic and interactive user interfaces in React without the complexities of managing state manually.

Remember that state updates with `useState` are asynchronous, so if you need to perform an action after the state has been updated, you might need to use the `useEffect` hook.