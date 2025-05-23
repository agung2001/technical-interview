Installation : `npm i redux-saga`

to understand how redux saga works you need to understand :
- [[Higher Order Function]]

## Sample : Simple API Call
<iframe width="560" height="315" src="https://www.youtube.com/embed/eA6rskkE9y8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Setup [main.jsx](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-simple-api-call/src/main.jsx)
```javascript
/** Setup Redux */  
import {Provider} from 'react-redux'  
import {combineReducers, createStore, applyMiddleware} from "redux";  
import createSagaMiddleware from 'redux-saga';  
import myFirstReducer from "./reducer";  
import mySaga from "./sagas";  
  
const sagaMiddleware = createSagaMiddleware();  
const rootReducer = combineReducers({myFirstReducer});  
const store = createStore(rootReducer, applyMiddleware(sagaMiddleware));  
sagaMiddleware.run(mySaga);
```

[actions.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-simple-api-call/src/actions.js) - This can be replaced by directly accessing the string
[reducer.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-simple-api-call/src/reducer.js) - This also unecessary already using middleware
[sagas.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-simple-api-call/src/sagas.js)
```javascript
import { takeEvery, call, put } from 'redux-saga/effects';  
import { GET_USER_FETCH, GET_USER_SUCCESS } from "./actions.js";  // this can be replaced by directly accessing the string "GET_USER_FETCH", etc
  
function usersFetch(){  
    return fetch('https://jsonplaceholder.typicode.com/users')  
    .then(response => response.json())  
}  
  
function* workGetUsersFetch(){  
    const users = yield call(usersFetch)  
    yield put({type: GET_USER_SUCCESS, users})  
}  
  
function* mySaga(){  
    yield takeEvery(GET_USER_FETCH, workGetUsersFetch);  
}  
  
export default mySaga;
```

[App.jsx](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-simple-api-call/src/App.jsx)
```javascript
import {useDispatch, useSelector} from "react-redux";  
import {getUserFetch} from "./actions.js";

function App() {  
    const dispatch = useDispatch();  
    const users = useSelector(state => state.myFirstReducer.users);
    ...

	return (
		<button onClick={() => dispatch(getUserFetch())}>Get Users</button>  
		<div> Users: {users.map((user) => (<div key={user.id}>{user.name}</div>) )} </div>
	)
}
  
export default App
```

## Sample : Using Redux Toolkit
<iframe width="560" height="315" src="https://www.youtube.com/embed/9MMSRn5NoFY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
Setup [main.jsx](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-redux-toolkit/src/main.jsx)
```javascript
/** Setup Redux */  
import {Provider} from 'react-redux'  
import createSagaMiddleware from 'redux-saga';  
import {configureStore} from '@reduxjs/toolkit'  
import catsReducer from './catSlice.js'  
import catSaga from './catSaga.js'

const sagaMiddleware = createSagaMiddleware();  
const store = configureStore({  
    reducer: {  
        cats: catsReducer  
    },  
    middleware: [sagaMiddleware]  
})  
sagaMiddleware.run(catSaga) 
```

[catSaga.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-redux-toolkit/src/catSaga.js)
```javascript
import {takeEvery, put, call} from 'redux-saga/effects';  
import { getCatsSuccess } from "./catSlice.js";  
  
function* workGetCatsFetch() {  
    const cats = yield call(() => fetch('https://api.thecatapi.com/v1/breeds'))  
    const formattedCats = yield cats.json()  
    const formattedCatsShortened = formattedCats.slice(0, 10);  
    yield put(getCatsSuccess(formattedCatsShortened));  
}  
  
function* catSaga() {  
    yield takeEvery('cats/getCatsFetch', workGetCatsFetch);  
}  
  
export default catSaga;
```

Act as a reducer - [catSlice.js](https://github.com/agung2001/hands-on-react-redux/blob/develop/projects/redux-saga-with-redux-toolkit/src/catSlice.js)
```javascript
import { createSlice } from "@reduxjs/toolkit";  
  
export const catSlice = createSlice({  
    name: "cats",  
    initialState: {  
        cats: [],  
        isLoading: false,  
    },  
    reducers: {  
        getCatsFetch: (state) => {  
            state.isLoading = true;  
        },  
        getCatsSuccess: (state, action) => {  
            state.cats = action.payload;  
            state.isLoading = false;  
        },  
        getCatsFailure: (state) => {  
            state.isLoading = false;  
        }  
    }  
})  
  
export const { getCatsFetch, getCatsSuccess, getCatsFailure } = catSlice.actions;  
  
export default catSlice.reducer;
```

## Resource
- [Official Website](https://redux-saga.js.org/)
- [GitHub - redux-saga/redux-saga](https://github.com/redux-saga/redux-saga)
- Boilerplate
	- [GitHub - maitraysuthar/react-redux-saga-boilerplate](https://github.com/maitraysuthar/react-redux-saga-boilerplate)