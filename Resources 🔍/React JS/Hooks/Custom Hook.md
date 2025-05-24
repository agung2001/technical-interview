A **custom hook** in React is a **JavaScript function** that allows you to **reuse logic** across multiple components. Custom hooks enable you to extract and share **stateful logic** or **side effects** without repeating code. They are a powerful feature that helps make your React components cleaner, more modular, and easier to maintain.

React custom hooks follow the **"rules of hooks"**, meaning they must:
- Be named starting with `use` (e.g., `useFetch`, `useCounter`).
- Be called at the top level of a component or hook (not inside loops, conditions, or nested functions).
- Only be called in React function components or other custom hooks.

Custom hooks allow you to encapsulate and reuse logic that would otherwise be written directly inside components.

### **Why Use Custom Hooks?**
1. **Code Reusability**:
    - Instead of repeating logic in multiple components, custom hooks allow you to extract that logic into reusable functions that can be shared among different components.
        
2. **Separation of Concerns**:
    - By moving logic (like state management, side effects, and event handling) out of the component and into a custom hook, your component becomes simpler and more focused on rendering the UI.
        
3. **Cleaner Code**:
    - Custom hooks allow you to organize your code more effectively, especially when dealing with complex logic, like data fetching, form handling, or animations.
        
4. **Better Testing**:
    - Custom hooks can be tested independently, making it easier to test logic without needing to deal with the whole component.

---

### **How to Create a Custom Hook**

A custom hook is just a regular JavaScript function that uses React’s built-in hooks (like `useState`, `useEffect`, etc.) to implement reusable logic.

#### **Example 1: Custom Hook for Handling Form Input**

Let's create a simple custom hook that manages form input values.

```javascript
import { useState } from 'react';

// Custom hook for form input
function useFormInput(initialValue) {
  const [value, setValue] = useState(initialValue);

  const handleChange = (e) => {
    setValue(e.target.value);
  };

  return {
    value,
    onChange: handleChange,
  };
}

export default useFormInput;
```

#### **Explanation**:

- **`useFormInput`** is a custom hook that manages the state of an input field.
- It takes an `initialValue` as an argument and returns the current value (`value`) and a `handleChange` function (`onChange`).
- This hook can be reused in any component that needs to manage form input.

Now, let’s use this custom hook in a component:

```javascript
import React from 'react';
import useFormInput from './useFormInput'; // Import custom hook

function MyForm() {
  const name = useFormInput(''); // Custom hook for name input
  const email = useFormInput(''); // Custom hook for email input

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', name.value, email.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Name:</label>
        <input type="text" {...name} />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" {...email} />
      </div>
      <button type="submit">Submit</button>
    </form>
  );
}

export default MyForm;
```

#### **Explanation**:
- The custom hook `useFormInput` is used to handle the state and behavior of both the `name` and `email` inputs.
- The `name` and `email` are now both managed by their respective custom hooks, making the form simpler and cleaner.
- The `value` and `onChange` properties returned by the custom hook are spread into the input fields (`{...name}` and `{...email}`) to link the inputs to the hook.

---

### **Example 2: Custom Hook for Fetching Data**
Now let’s create a custom hook that handles data fetching. This is a very common use case for custom hooks in React.

```javascript
import { useState, useEffect } from 'react';

// Custom hook for data fetching
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]); // Re-run the effect if the URL changes

  return { data, loading, error };
}

export default useFetch;
```

#### **Explanation**:
- The **`useFetch`** custom hook fetches data from a given URL.
- It tracks the `data`, `loading`, and `error` states.    
- It uses `useEffect` to fetch the data when the component first renders and when the `url` changes.
- This custom hook returns an object with `data`, `loading`, and `error` so that the component can handle the UI based on these values.

Now, let’s use this custom hook in a component:
```javascript
import React from 'react';
import useFetch from './useFetch'; // Import custom hook

function DataDisplay() {
  const { data, loading, error } = useFetch('https://api.example.com/data'); // Custom hook for fetching data

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Error: {error.message}</p>;
  }

  return (
    <div>
      <h1>Fetched Data:</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default DataDisplay;
```

#### **Explanation**:
- The `useFetch` hook is used to fetch data from an API endpoint.
- The component displays a loading message while the data is being fetched.
- If there’s an error, it displays the error message.
- Once the data is successfully fetched, it’s displayed in a formatted JSON.

---

### **When to Use Custom Hooks**
1. **Reusing State Logic**: Custom hooks are perfect for extracting and reusing stateful logic that can be shared across components. This can include form handling, event handling, and data fetching.
2. **Handling Side Effects**: If multiple components need the same logic for handling side effects (like timers, localStorage interactions, etc.), custom hooks can help you centralize that logic.
3. **Separation of Concerns**: Custom hooks allow you to separate the logic of the component from the component’s presentation, making components cleaner and easier to maintain.
4. **Complex Logic**: When the state and logic of your component grow complex, custom hooks allow you to break down that logic into smaller, manageable pieces.

---

### **Best Practices for Custom Hooks**
- **Keep it reusable**: Custom hooks should be designed to be reused across multiple components, so keep them general and flexible.
- **Keep it simple**: If your hook is doing too much, it’s a sign that it might be better to split it into smaller hooks.
- **Name it properly**: Always prefix your custom hook names with `use` (e.g., `useFormInput`, `useFetch`) so that it’s clear they are hooks.
- **Avoid side effects in custom hooks**: Keep side effects (like `useEffect`) inside custom hooks to keep the component code clean.

### **Conclusion**

A **React custom hook** is a JavaScript function that allows you to reuse **stateful logic** or **side effects** across multiple components. Custom hooks help to make your components cleaner, more modular, and maintainable by encapsulating common logic that can be shared across components.

By using custom hooks, you can avoid code duplication, improve the readability of your components, and manage complex logic outside of the UI rendering logic, making your application easier to maintain as it grows.

## Resource
- GitHub
	- [antonioru/beautiful-react-hooks](https://github.com/antonioru/beautiful-react-hooks) : 8.3 k
	- [streamich/react-use](https://github.com/streamich/react-use) : 43.k
	- [uidotdev/usehooks](https://github.com/uidotdev/usehooks) : 10.6 k