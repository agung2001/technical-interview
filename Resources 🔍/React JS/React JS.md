<iframe width="560" height="315" src="https://www.youtube.com/embed/Tn6-PIqc4UM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
**React JS** is a popular JavaScript library for building user interfaces, particularly for single-page applications (SPAs) where you need a fast, dynamic, and interactive web experience. It was developed by Facebook and has since become one of the most widely used front-end technologies.

Here's a breakdown of key concepts in React JS:

## **Component-Based Architecture**
- React allows developers to build reusable UI components, making the code more modular and maintainable.
- Each component can manage its state and render dynamic content based on that state.
- Components can be nested inside other components to create complex UIs.

## **Virtual DOM**
- React uses a "Virtual DOM," which is an in-memory representation of the actual DOM on the web page.
- When there are changes to the UI, React first updates the Virtual DOM and then compares it with the actual DOM. This process is called **reconciliation**.
- React only updates the parts of the DOM that have actually changed, leading to better performance compared to directly manipulating the DOM.

## Declarative vs Imperative
- Declarative : Modifying DOM
	- React JS run declarative, but using of a blueprint or state changes based on how the app should look like
- Imperative : Listen to the change of event

## **JSX (JavaScript XML)**
- React uses JSX, a syntax extension for JavaScript that allows you to write HTML-like code within JavaScript.
- JSX makes it easier to visualize and define how the UI will look and behave.
- Example:
    ```jsx
    const element = <h1>Hello, world!</h1>;
    ```

## **State and Props**
- **State**: Represents data that can change over time and affect how a component renders.
- **Props**: Short for "properties," props are used to pass data from one component to another. They are immutable and are set by the parent component.

- Example:
    ```jsx
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    ```
    
    Here, `props.name` is passed from a parent component.

## **One-Way Data Flow**
![](https://kinsta.com/wp-content/uploads/2021/11/react-one-way-data-flow.jpg)

- React follows a one-way data flow, meaning data is passed from parent to child components via props.
- This predictable flow of data makes debugging and state management simpler.

## **Lifecycle Methods**
![](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/ogimage.png)

- React components have lifecycle methods that allow you to run code at specific points during the component's life (e.g., when it is created, updated, or destroyed).
- Examples include `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

## **React Hooks**
- Introduced in React 16.8, **Hooks** allow functional components to manage state, lifecycle methods, and side effects without using class-based components.
- Common hooks include `useState`, `useEffect`, and `useContext`.
    ```jsx
    const [count, setCount] = useState(0);
    ```
    
    This is an example of using the `useState` hook to manage state in a functional component.

## Concepts
- [Components and Props](https://reactjs.org/docs/components-and-props.html)
- [State and Lifecycles](https://reactjs.org/docs/state-and-lifecycle.html) 
- [Handling Events](https://reactjs.org/docs/handling-events.html)
- [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
- Method Binding : [[React & Redux#Method Binding]]
- Stateless Component : [[React & Redux#Stateless Components]]
- Higher Order Component : [[React & Redux#Higher Order Component]]
- [Lazy Loading](https://react.dev/reference/react/lazy)
	- [Suspense](https://react.dev/reference/react/Suspense)

## Functional Components and Class Components
this is a fundamental concept on how to define component in react, to learn more you can read it [here](https://www.geeksforgeeks.org/differences-between-functional-components-and-class-components-in-react/)

- **Class component** is a way to define a component using the ES6 class syntax. It allows you to use class methods and the lifecycle methods provided by React.
```javascript
class Simple extends React.component {...}
```

- **Functional component** is a way to define a component using the arrow function syntax. A functional component is a simple JavaScript function that takes in `props` (properties) as an argument and returns a React element. It is a simpler way of defining a component and it's good for simple components that only need to render some UI based on the props they receive.
```javascript
const Simple = () => {...}
```

## Tricks
- Code Splitting : 
	- [How to Improve Performance in React with Code Splitting](https://www.youtube.com/watch?v=-4fyyyQjsz8)
	- [Speed Up Your React Apps With Code Splitting](https://www.youtube.com/watch?v=JU6sl_yyZqs)

## Tutorial
- Prelimineries
	 - [Web Dev Simplified - Do You Know Enough JavaScript To Learn React](https://www.youtube.com/watch?v=JR9wsVYp8RQ)
- Tutorials
	- [Net Ninja - Full Modern React Tutorial](https://www.youtube.com/watch?v=j942wKiXFu8&list=PL4cUxeGkcC9gZD-Tvwfod2gaISzfRiP9d)
	- [Prawito Hudoro - ReactJS Tutorial](https://www.youtube.com/watch?v=5kHyviqjhCk&list=PLU4DS8KR-LJ03qEsHn9zV4qdhcWtusBqb)
	- [Web Dev Simplified - Learn React In 30 Minutes](https://www.youtube.com/watch?v=hQAHSlTtcmY)
	- [React Router Tutorial - 14 - Lazy Loading](https://www.youtube.com/watch?v=MJn4W7pR6RU)
- Projects
	- [Build and Deploy 4 Modern React Apps and Get Hired as a Frontend Developer | Full 10-Hour Course](https://www.youtube.com/watch?v=F627pKNUCVQ&list=WL)
	- [Let's Build ChatGPT 2.0 with React JS and OpenAI on your PC!](https://www.youtube.com/watch?v=qwM23_kF4v4&list=WL)

## Resources
- [Official Website](https://reactjs.org/)
	- [Documentation](https://reactjs.org/docs/getting-started.html)
- [W3Schools - React JS](https://www.w3schools.com/REACT/DEFAULT.ASP)