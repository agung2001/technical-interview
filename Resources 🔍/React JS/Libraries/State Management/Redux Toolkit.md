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