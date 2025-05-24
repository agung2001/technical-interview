**Code Splitting** is a powerful technique in **React** (and other modern JavaScript frameworks) used to **split** a large bundle of JavaScript code into smaller, more manageable pieces that can be loaded **on demand**. This technique allows for better performance and faster load times for web applications by only loading the necessary code for the current view or interaction.

### Why is Code Splitting Important?

When building modern web applications, especially large-scale apps, the JavaScript bundle that gets generated can become quite large. This can negatively impact performance, particularly when users first load the application. With **Code Splitting**, you can break the application into smaller chunks (or bundles) that are loaded only when they are needed, reducing the initial load time and improving the user experience.

### How Code Splitting Works:

1. **Dynamic Importing**: Code splitting relies on **dynamic imports**—a way of loading JavaScript modules asynchronously. Instead of including everything in a single bundle, you only load the code for a specific page or feature when needed.
    
2. **Lazy Loading**: React supports a concept called **lazy loading**, which allows you to load parts of your app lazily (only when required). For example, a page that a user might never visit will not be loaded initially. Instead, the required code will be fetched when the user navigates to that page.
    
3. **Webpack and React**: Tools like **Webpack** and **React's built-in features** allow you to set up code splitting in an easy and efficient way.
    

### Example of Code Splitting in React:

#### Using `React.lazy()` and `Suspense`:

React provides the `React.lazy()` function to load components lazily. This is one of the easiest ways to implement code splitting in a React app.

- **`React.lazy()`**: It enables you to dynamically import a component when it's needed.
    
- **`Suspense`**: It's used to show a loading indicator while the lazily loaded component is being fetched.
    

#### Example Code:

```javascript
import React, { Suspense } from 'react';

// Lazily load the component
const LazyLoadedComponent = React.lazy(() => import('./LazyLoadedComponent'));

const App = () => {
  return (
    <div>
      <h1>Welcome to Code Splitting in React!</h1>

      {/* Suspense component to show loading state */}
      <Suspense fallback={<div>Loading...</div>}>
        <LazyLoadedComponent />
      </Suspense>
    </div>
  );
};

export default App;
```

#### Explanation:

1. **`React.lazy()`** is used to dynamically import the `LazyLoadedComponent` only when it is needed.
    
2. **`Suspense`** wraps the lazily loaded component and provides a fallback UI (in this case, a loading message) while the component is being fetched.
    
3. When the `LazyLoadedComponent` is required (in this case, when it is rendered), it will be loaded asynchronously, and once it's loaded, it will be displayed.
    

### Code Splitting by Route (React Router Example):

For larger applications, code splitting is commonly used at the route level. When a user navigates to a new route, only the code for that route is loaded.

#### Example Using React Router:

```javascript
import React, { Suspense } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

// Lazy load routes
const HomePage = React.lazy(() => import('./HomePage'));
const AboutPage = React.lazy(() => import('./AboutPage'));

const App = () => {
  return (
    <Router>
      <Suspense fallback={<div>Loading...</div>}>
        <Switch>
          <Route exact path="/" component={HomePage} />
          <Route path="/about" component={AboutPage} />
        </Switch>
      </Suspense>
    </Router>
  );
};

export default App;
```

#### Explanation:

1. **Route-Level Code Splitting**: `HomePage` and `AboutPage` are both lazily loaded when the user navigates to the corresponding route.
    
2. **`Suspense`** is used to show a loading state while the new page’s component is being loaded.
    

### Other Techniques for Code Splitting:

Besides **React.lazy()**, there are other ways to implement code splitting:

1. **Dynamic `import()`**:
    
    - In Webpack, you can use the **dynamic `import()`** syntax to split large bundles manually. This works in both React and non-React JavaScript projects.
        
    
    Example:
    
    ```javascript
    import(/* webpackChunkName: "moduleName" */ './MyModule')
      .then((module) => {
        // Use the module here
      })
      .catch((error) => console.error('Error loading module:', error));
    ```
    
2. **Webpack Configuration**:
    
    - Webpack automatically splits code into separate bundles based on the dynamic imports and the entry points. You can customize how Webpack handles code splitting in its configuration.
        
3. **React Router with `React.lazy()`**:
    
    - For routing-based code splitting, React Router works seamlessly with `React.lazy()` to split out bundles per route.
        

### Benefits of Code Splitting:

1. **Improved Load Times**:
    
    - Code splitting helps reduce the initial load time of your application by loading only the necessary JavaScript for the page that the user is currently viewing. This can lead to faster performance, especially for large apps.
        
2. **Efficient Resource Loading**:
    
    - Resources are loaded only when they are needed, which reduces the amount of JavaScript that needs to be downloaded initially, making the app feel faster.
        
3. **Better User Experience**:
    
    - With lazy loading, users can start interacting with the application faster since they don’t need to wait for the entire application to load upfront.
        
4. **Smaller Bundles**:
    
    - Code splitting allows you to break large bundles into smaller pieces, which can be cached more effectively by the browser. This means that only new or updated chunks need to be fetched when the user returns to your app.
        

### Potential Challenges:

1. **Overhead of Network Requests**:
    
    - Code splitting can introduce overhead from multiple network requests as JavaScript bundles are loaded separately. However, with proper caching strategies, this can be minimized.
        
2. **SEO**:
    
    - If you're building a single-page app (SPA) and rely heavily on JavaScript, code splitting might make it more difficult to render SEO-friendly content, though this can be mitigated with **server-side rendering (SSR)** or **static site generation (SSG)** (as with Next.js).
        
3. **Complexity in Large Applications**:
    
    - Code splitting adds complexity in managing how and when different bundles are loaded, particularly when working with large and complex applications with multiple routes and components.
        

### Conclusion:

**Code splitting** is a powerful optimization technique in modern web development, especially for large applications. It helps improve performance by loading only the necessary JavaScript code for the current view, which reduces the initial load time. React provides built-in support for code splitting through `React.lazy()` and `Suspense`, and additional techniques like **Webpack’s dynamic import** can also be used. While code splitting offers significant performance benefits, it requires careful management to avoid unnecessary complexity or performance pitfalls.

## Resource
- Conference
	- [Neehar Venugopal - A Beginner's Guide to Code Splitting Your React App - React Conf 2017](https://www.youtube.com/watch?v=bb6RCrDaxhw)
- [Dynamic Importing (Code-Splitting) | ES2020](https://www.youtube.com/watch?v=93R57sLATM4)
- [How to make your JavaScript Bundle Smaller](https://www.youtube.com/watch?v=kwUfeWe7DCw)
- [How to Improve Performance in React with Code Splitting](https://www.youtube.com/watch?v=-4fyyyQjsz8)
- [Speed Up Your React Apps With Code Splitting](https://www.youtube.com/watch?v=JU6sl_yyZqs)