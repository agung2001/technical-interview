**Redux Toolkit** is an official library for **Redux**, designed to simplify and streamline the process of managing state in JavaScript applications, especially when using **React**. Redux Toolkit provides a set of tools and best practices that make it easier to configure, write, and maintain Redux logic by reducing boilerplate code, improving performance, and enhancing developer experience.

### Why Use Redux Toolkit?

1. **Reduces Boilerplate**: Traditional Redux requires a lot of repetitive boilerplate code, including defining actions, action creators, reducers, and store configuration. Redux Toolkit helps reduce this boilerplate by providing built-in utilities for creating actions and reducers with minimal code.
    
2. **Encourages Best Practices**: Redux Toolkit promotes the **standardized approach** for Redux implementation, including how to structure slices of state, handle asynchronous logic, and configure the store. This leads to **more maintainable and scalable applications**.
    
3. **Simplifies Asynchronous Logic**: Redux Toolkit comes with the **createAsyncThunk** API to manage asynchronous actions (e.g., fetching data from APIs) easily, without the need to manually dispatch actions for pending, success, and failure states.
    
4. **Pre-configured Store**: It comes with a pre-configured store setup that includes common middleware like **Redux Thunk** for handling asynchronous actions, as well as devtools for easier debugging.
    

---

### Key Features of Redux Toolkit:

1. **`createSlice`**:
    
    - `createSlice` is the core function in Redux Toolkit that allows you to define **actions** and **reducers** together in one place, reducing the need to define action types, action creators, and reducers manually.
        
    
    **Example of `createSlice`**:
    
    ```javascript
    import { createSlice } from '@reduxjs/toolkit';
    
    // Define an initial state
    const initialState = {
      value: 0,
    };
    
    // Create a slice of the Redux state
    const counterSlice = createSlice({
      name: 'counter', // The name of this slice
      initialState,     // Initial state of the slice
      reducers: {       // Reducers define how the state updates
        increment: (state) => {
          state.value += 1;
        },
        decrement: (state) => {
          state.value -= 1;
        },
      },
    });
    
    // Export actions for dispatching
    export const { increment, decrement } = counterSlice.actions;
    
    // Export the reducer to be included in the store
    export default counterSlice.reducer;
    ```
    
    In this example, the `createSlice` function automatically generates the action creators (e.g., `increment`, `decrement`) and reducers for handling actions.
    
2. **`configureStore`**:
    
    - `configureStore` is used to set up the Redux store with default settings and middleware (like Redux Thunk). It simplifies the process of creating the Redux store by handling common configurations such as adding middleware and integrating devtools.
        
    
    **Example of `configureStore`**:
    
    ```javascript
    import { configureStore } from '@reduxjs/toolkit';
    import counterReducer from './counterSlice';
    
    const store = configureStore({
      reducer: {
        counter: counterReducer,
      },
    });
    
    export default store;
    ```
    
    Here, `configureStore` sets up the store with the `counterReducer` and automatically includes the necessary middleware for asynchronous actions.
    
3. **`createAsyncThunk`**:
    
    - `createAsyncThunk` simplifies the process of dispatching actions for asynchronous logic. It generates action creators for handling the lifecycle of asynchronous requests (such as **pending**, **fulfilled**, and **rejected** states) and automatically dispatches those actions.
        
    
    **Example of `createAsyncThunk`**:
    
    ```javascript
    import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
    
    // Create an async action to fetch data
    export const fetchData = createAsyncThunk(
      'data/fetchData',
      async (url) => {
        const response = await fetch(url);
        return response.json();
      }
    );
    
    const dataSlice = createSlice({
      name: 'data',
      initialState: {
        data: [],
        status: 'idle',
      },
      reducers: {},
      extraReducers: (builder) => {
        builder
          .addCase(fetchData.pending, (state) => {
            state.status = 'loading';
          })
          .addCase(fetchData.fulfilled, (state, action) => {
            state.status = 'succeeded';
            state.data = action.payload;
          })
          .addCase(fetchData.rejected, (state) => {
            state.status = 'failed';
          });
      },
    });
    
    export default dataSlice.reducer;
    ```
    
    In this example:
    
    - `createAsyncThunk` handles the asynchronous fetch logic and generates three actions: `pending`, `fulfilled`, and `rejected`.
        
    - The `extraReducers` field in `createSlice` allows you to handle the lifecycle states (`pending`, `fulfilled`, `rejected`) directly inside the slice.
        
4. **`createEntityAdapter`**:
    
    - `createEntityAdapter` is a utility function in Redux Toolkit to simplify managing collections of data (like lists of items or entities) in your Redux store. It automatically handles tasks like **adding**, **updating**, and **removing** items in a normalized state.
        
    
    **Example of `createEntityAdapter`**:
    
    ```javascript
    import { createSlice, createEntityAdapter } from '@reduxjs/toolkit';
    
    const usersAdapter = createEntityAdapter();
    
    const initialState = usersAdapter.getInitialState();
    
    const usersSlice = createSlice({
      name: 'users',
      initialState,
      reducers: {
        userAdded: usersAdapter.addOne,
        userRemoved: usersAdapter.removeOne,
      },
    });
    
    export const { userAdded, userRemoved } = usersSlice.actions;
    export default usersSlice.reducer;
    ```
    
    This example simplifies managing a collection of users, with automatic functions for adding, removing, and updating items.
    
5. **Development Tools**:
    
    - Redux Toolkit works seamlessly with **Redux DevTools**, allowing you to easily debug your application's state changes using the browser's DevTools extension.
        

---

### Benefits of Redux Toolkit:

1. **Simplified Setup**:
    
    - Redux Toolkit abstracts away much of the boilerplate required for setting up Redux, such as defining action types and action creators, and configuring the store. This reduces the initial setup time for developers.
        
2. **Less Boilerplate**:
    
    - By using utilities like `createSlice`, `createAsyncThunk`, and `createEntityAdapter`, Redux Toolkit significantly reduces the amount of code needed for creating actions, reducers, and handling asynchronous logic.
        
3. **Built-in Best Practices**:
    
    - Redux Toolkit encourages best practices by using `Immer` (a library for handling immutable state updates) internally, making it easier to handle state updates without needing to manually copy and modify state objects.
        
4. **Integration with Modern JavaScript Features**:
    
    - Redux Toolkit leverages **modern JavaScript features** such as async/await, destructuring, and ES Modules, making the Redux code more concise, readable, and maintainable.
        
5. **Better Developer Experience**:
    
    - With built-in support for **Redux DevTools**, **debugging** and **inspecting the Redux state** becomes much easier. Additionally, the simplified API and enhanced documentation help developers get started quickly.
        

## Installation
Installation : `npm i @reduxjs/toolkit`

## Sample PizzaSlice
<iframe width="560" height="315" src="https://www.youtube.com/embed/_shA5Xwe8_4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
- see [[React Redux]] to set initial configuration

[pizzaSlice.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-in-100-seconds/src/pizzaSlice.js)
```javascript
import { createSlice } from "@reduxjs/toolkit";  
  
const initialState = {  
    toppings: ['pepperoni', 'sausage', 'onion', 'mushroom'],  
    gluten: true,  
}  
  
export const pizzaSlice = createSlice({  
    name: 'pizza',  
    initialState,  
    reducers: {  
        toggleGluten: (state) => {  
            state.gluten = !state.gluten;  
        },  
        addTopping: (state, action) => {  
            state.toppings = [...state.toppings, action.payload];  
        },  
    },  
});  
  
export const { toggleGluten, addTopping } = pizzaSlice.actions;  
export default pizzaSlice.reducer;
```

[App.jsx](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-in-100-seconds/src/App.jsx)
```javascript
import {useSelector, useDispatch} from 'react-redux';  
import {addTopping} from "./pizzaSlice.js";

function App() {  
    const pizza = useSelector(state => state.pizza);  
    const dispatch = useDispatch();

	return (
		...
		{pizza.toppings.map(topping => (  
		    <div key={topping}>{topping}</div>  
		))}  
		  
		<button onClick={() => dispatch(addTopping('cheese'))}>  
		    Add Cheese  
		</button>
	)
}

export default App
```

## Sample Counter
<iframe width="560" height="315" src="https://www.youtube.com/embed/ANnQ7Z7A1PU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Resource
- [Official Website](https://redux-toolkit.js.org/)