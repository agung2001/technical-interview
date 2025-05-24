A **Higher Order Component (HOC)** is a pattern in React used to reuse component logic. It's a function that takes a component and returns a new component with additional props or functionality. HOCs do not modify the original component but instead create a wrapper around it, allowing for code reuse and modularity.

### How it works:
- A Higher Order Component takes a component as an argument.
- It enhances or modifies the behavior of the component by adding extra functionality, like state, lifecycle methods, or event handling.
- It returns a new component with these additional capabilities.

### Key Points:
1. **Pure Functions**: HOCs are pure functions, meaning they don’t mutate the original component. They only return a new component with added behavior.
2. **No Side Effects**: HOCs should not modify the passed component’s state or props directly. Instead, they should rely on props to add new logic.
3. **Reusability**: HOCs allow for the reuse of logic across different components, improving code organization and maintainability.

### Example:

Let’s say we have a simple component:

```javascript
const MyComponent = ({ name }) => <div>Hello, {name}!</div>;
```

We can create a higher order component to add extra logic, such as logging every time the component renders:

```javascript
const withLogging = (Component) => {
  return (props) => {
    console.log('Rendering component with props:', props);
    return <Component {...props} />;
  };
};
```

Now, if we wrap `MyComponent` with `withLogging`, it will log every time it renders:

```javascript
const MyComponentWithLogging = withLogging(MyComponent);

// Usage
<MyComponentWithLogging name="John" />;
```

In this case, `withLogging` is the HOC, and it adds the logging functionality to `MyComponent`.

### Common Use Cases for HOCs:
- **Authentication**: Wrapping a component with an HOC that checks if the user is authenticated.
- **Conditional Rendering**: Wrapping components with an HOC to conditionally render based on certain props or state.
- **Error Boundaries**: Wrapping components with error handling logic.

HOCs allow you to compose logic without changing the core structure of your components, promoting a more modular and clean codebase.

## Resource
- [React Reference - Higher-Order Components](https://legacy.reactjs.org/docs/higher-order-components.html)