React Redux is the official React UI bindings layer for Redux. It lets your React components read data from a Redux store, and dispatch actions to the store to update state. [Read More](https://react-redux.js.org/introduction/getting-started)

Installation : `npm i react-redux`

## Configuration
[main.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-in-100-seconds/src/main.jsx)
```javascript
/** Setup redux */  
import store from "./store.js";  
import { Provider } from 'react-redux'  

/** Wrap Root with Redux Provider */
ReactDOM.createRoot(document.getElementById('root')).render(  
    <React.StrictMode>  
        <Provider store={store}>  
            <App />  
        </Provider>  
    </React.StrictMode>  
)
```

[store.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-in-100-seconds/src/store.js)
```javascript
import {configureStore} from "@reduxjs/toolkit";  
import pizzaReducer from "./pizzaSlice";  
  
export default configureStore({  
    reducer: {  
        pizza: pizzaReducer,  
    }  
});
```

## Samples
- [GitHub - agung2001/hands-on-react-redux](https://github.com/agung2001/hands-on-react-redux)
- [[React & Redux#Introduction to Redux]]

## Resource
- [Official Website](https://react-redux.js.org/)
- [NPM](https://www.npmjs.com/package/react-redux)