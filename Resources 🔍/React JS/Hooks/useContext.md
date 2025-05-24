The `useContext` hook is one of the **React hooks** that allows you to **consume** and access **context** in a functional component. It provides a way to share values (like data or functions) across your component tree without needing to manually pass props through every level of the component hierarchy.

Context is often used for global data, such as themes, authentication, language preferences, or user settings, which need to be accessible by many components across the application.

### **What is Context in React?**
**React Context** is a way to pass data through the component tree without having to explicitly pass props down through every level. You can create a **Context** with the `React.createContext()` method, which returns a **Provider** and a **Consumer**.
- **Provider**: This component provides the context value to all components in the tree that are descendants of it.
- **Consumer**: The consumer component accesses the context value, but in modern React (v16.8+), the `useContext` hook is used to access context values instead of `Consumer`.

The `useContext` hook simplifies consuming context values inside functional components.

### **How to Use `useContext`**

#### **1. Create a Context**
To use `useContext`, first, you need to create a context. This is done using the `React.createContext()` method.

```javascript
import React, { createContext } from 'react';

// Create a context with a default value
const ThemeContext = createContext('light'); // Default theme is 'light'
```

- Here, `ThemeContext` is a context that will hold a value (`light` by default).

#### **2. Provide Context Using the Provider**
Next, you need to wrap a part of your component tree with the **Provider** component. The `value` prop of the `Provider` will contain the data you want to share with the components that consume the context.

```javascript
import React from 'react';
import { ThemeContext } from './ThemeContext'; // Import the context

function App() {
  return (
    <ThemeContext.Provider value="dark"> {/* Set the theme value */}
      <Navbar />
      <MainContent />
    </ThemeContext.Provider>
  );
}

export default App;
```

- In this example, the `App` component wraps the `Navbar` and `MainContent` components with the `ThemeContext.Provider`. The value `"dark"` is passed to the `value` prop, so all child components can access this value.

#### **3. Consume Context with `useContext`**
To consume the context in a child component, you use the `useContext` hook, which retrieves the value from the nearest **Provider** in the component tree.

```javascript
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext'; // Import the context

function Navbar() {
  const theme = useContext(ThemeContext); // Consume the context value

  return (
    <nav className={theme}>
      <h1>Welcome to my website</h1>
    </nav>
  );
}

export default Navbar;
```

- Here, the `Navbar` component uses `useContext(ThemeContext)` to retrieve the current theme (`dark` in this case) and applies it to the `className` of the `nav` element.
- The `useContext` hook accesses the `ThemeContext` and automatically provides the `dark` value (the context value provided in the `App` component).

### **Why Use `useContext`?**

Without `useContext`, you would have to pass the `theme` value as a prop from `App` to every component in the tree (e.g., `App` → `Navbar` → `MainContent`), even if these components don’t need to modify or access the `theme` value. This can quickly become cumbersome and inefficient.

With `useContext`, you can avoid prop drilling (passing props through many levels of the component tree) and directly access the value you need.

### **Real-World Use Cases for `useContext`**

1. **Theme Management**:
    - You can use `useContext` to manage and apply theme settings (e.g., dark mode or light mode) globally throughout your app.
    
    Example:
    
    ```javascript
    const ThemeContext = createContext('light');
    ```
    
2. **User Authentication**:
    - You can store the authentication status of the user in context and provide it across your app, allowing components to easily check if a user is logged in and display appropriate UI.
    
    Example:
    
    ```javascript
    const UserContext = createContext(null);
    ```
    
3. **Language and Localization**:
    - You can store the current language setting and provide localized strings or content based on the selected language throughout the app.
    
    Example:
    
    ```javascript
    const LanguageContext = createContext('en');
    ```

### **Example of a Complete `useContext` Implementation**

Let’s put everything together with a simple example of **theme switching** (light/dark mode):

```javascript
import React, { useState, useContext, createContext } from 'react';

// Create the ThemeContext with a default value of 'light'
const ThemeContext = createContext('light');

function ThemeToggle() {
  const theme = useContext(ThemeContext);  // Get the current theme
  const setTheme = useContext(ThemeContext); // Set the theme (we’ll update this part later)

  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Toggle Theme (Current: {theme})
    </button>
  );
}

function App() {
  const [theme, setTheme] = useState('light'); // Manage theme state

  return (
    <ThemeContext.Provider value={theme}>
      <div className={theme}>
        <h1>Welcome to my App!</h1>
        <ThemeToggle />
      </div>
    </ThemeContext.Provider>
  );
}

export default App;
```

### **How This Works**:
1. **Creating Context**: We create the `ThemeContext` using `createContext()` with a default value of `'light'`.
2. **Providing Context**: In the `App` component, we wrap the part of the UI that needs the theme (the entire app, in this case) with the `ThemeContext.Provider` and set its value to the current `theme`.
3. **Consuming Context**: The `ThemeToggle` button consumes the theme value using the `useContext` hook, and allows users to toggle between `'light'` and `'dark'` mode by clicking the button.

### **Advantages of `useContext`**
1. **Avoids Prop Drilling**: `useContext` eliminates the need to pass props down through several layers of components, making it easier to manage and share global data.
2. **Cleaner Code**: It simplifies state management and avoids repetitive code for passing values through many components.
3. **Scalability**: As your app grows, `useContext` helps you manage and access shared state (like user authentication or theme) across the app more effectively.

## Resource
- [React Reference - useContext](https://react.dev/reference/react/useContext)