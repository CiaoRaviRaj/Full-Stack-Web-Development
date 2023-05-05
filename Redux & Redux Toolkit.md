# Redux & Redux Toolkit

## Introduction

- javascript library
- predictable state container ( global level state container )
- Redux Toolkit is cut off redux boil plant code.
- React-Redux is the official Redux UI binding library of React

## Getting Started

- setup node package
    
    ```jsx
    npm init -y
    ```
    
- Install Redux
    - 
    
    ```jsx
    npm install redux
    ```
    
- Create index.js file in root directory

## Three Core Concept

- Store ( hold
    - Holds the state
- Action
    - describes what happened
- Reducer
    - handle the action and decides how to update the state

## Principle of Redux ( pattern )

- all global state is an object store  inside a single store.
- dispatch an action to update state
    - state is read only (not updated directly)
- Pure Reducer to used for update the state
    - Reducer - (previousState, action) ⇒ updateState

## Actions

- String Const → Type
    
    ```jsx
    const CAKE_ORDERED = ‘CAKE_ORDERED
    ```
    
- Action function

```jsx
function orederedCake(qty = 1) {
	return {
			type: CAKE_ORDERED,
			payload: qty,
	}
}
```

## Reducers

- PreviousState , action are need for reducer
- state is an object
    
    ```jsx
    const initialState = {
    numberOfCake: 10,
    }
    ```
    
- Reducer Function
    
    ```jsx
    const reducer = (state = initialState, action) => {
    	switch (action.type) {
    		case CAKE_ORDERED: 
    				return {
    					...state,
    					numberOfCake: state.numberOfCake - action.payload
    				}
    			default: 
    					return state
    	}
    	
    ```
    
- 

## Store

- Hold application state
    
    ```jsx
    import redux from 'redux'
    const store = redux.createStore(reducers))
    ```
    
- Allow access to state via getState()
    
    ```jsx
    console.log('Initial state',store.getState())
    ```
    
- Allow state to be update via dispatch(action)
    
    ```jsx
    store.dispatch(orederCake())
    store.dispatch(orederCake(3))
    ```
    
- Registers listeners via subscribe(listener)
    
    ```jsx
    store.subscribe(() => console.log('update state',store.getState())
    
    ```
    
- Handles unregistering of listeners via the function returned by subscribe(listener)
    
    ```jsx
    const unsubscribe = store.subscribe(() => console.log('update state',store.getState())
    
    unsubscribe()
    ```
    

## bindActionCreators

- it is used to bind a variable for all mention actions

```jsx
const bindActionCreators = redux.bindActionCreators

const actions = bindActionCreators({ ordercake, restockCake}, store.dispatch)
actions.orderCake()
actions.orderCake()
actions.restockCake(3)

```

## Multiple Reducer And Combine Reduce

- initial state separate from different reducer
    
    ```jsx
    const increameInitialState = {
    	numberOfIncreame = 10
    }
    ```
    
- separate reducer
    
    ```jsx
    // to normal reduce action for
    
    ```
    
- Combine reducer
    
    ```jsx
    const combineReducers = redux.combineReducers
    
    // Before create store
    
    const rootReducer = combineReducers({
    	cake: cakeReducer,
    	icecream: increamReducer
    })
    
    // In Store we just pass Root reducer
    const store = createStore(rootReducer)
    ```
    

## Immer

- nested-state update is pain full
- npm i immer
- const produce = require(’immer’).produce
- in reducer function
    - return produce(state, (draft) ⇒ {
        
        # it is look like it mutated the state but it return new object underhood
        
        - draft.address.street = action.payload
    - }

## Middleware

- it is used for logging , crash reporting , performing asynchronous tasks
- we are using Redux-logger
    - npm i ‘redux-logger’
    - const ReduxLogger = require(’redux-logger’)
    - const logger = reduxLogger.createLogger()
    - const applyMiddleware = redux.applyMiddleware
    - const store = createStore(rootReducer, applyMiddleware(logger))
    - it just log the store
    - it work as subscribe and unsubscribe
- Async Actions
    - if you dispatch action , it do synchronous directly
    - we do API Call in actions , it is an async actions
        
        ```jsx
        import redux from 'redux'
        const createStore = redux.createStore
        
        // Initial State
        const initialState = {
        	loading : false,
        	users: [],
        	error: ''
        }
        
        const FETCH_USERS_REQUESTED = 'FECTH_USERS_REQUESTED'
        const FETCH_USERS_SUCCEEDED = 'FETCH_USERS_SUCCEEDED'
        const FETCH_USERS_FAILED = 'FETCH_USERS_FAILED'
        
        // Actions Creators
        const fetchUsersRequest = () => {
        	return {
        		type: FETCH_USERS_REQUESTED
        	}
        }
        const fetchUsersSuccess = (users) => {
        	return {
        		type: FETCH_USERS_SUCCEEDED,
        		payload: users
        	}
        }
        const fetchUsersError = (error) => {
        	return {
        		type: FETCH_USERS_FAILED,
        		payload: error
        	}
        }
        
        // reducer function
        
        const reducer = (state = initalState, action) => {
        	switch (action.type):
        		case FETCH_USERS_REQUESTED:
        			return {
        				...state,
        				loading: true
        			}
        		case FETCH_USERS_SUCCEEDED: 
        			return {
        				...state,
        				users: action.payload,
        				error: '',
        			}
        		case FETCH_USERS_FAILED: 
        			return {
        				...state,
        				users: [],
        				error: action.payload,
        			}
        		default : 
        			return state
        }
        
        // create store
        const store = createStore(reducer)
        
        ```
        
    - redux-thunk
        - npm i redux-thunk
        
        ```jsx
        const thunkMiddleware = require('redux-thunk').default
        const applyMiddleware = redux.appyMiddleware
        
        const store = createStore(reducer, appyMiddleware(thunkMiddleware))
        
        // Async Actions creator
        const fetchUsers = () => {
        	return function(dispatch) {
        		//dispatch 1
        		dispatch(fetchUserRequest())
        		axios.get('apiUrl')
        			.then(response => {
        				//dispatch 1
        				const users = response.data.map((user) => user.id)
        				dispatch(fetchUserSuccess(users))
        			})
        			.catch((error) => {
        				//dispatch 1
        				dispatch(fetchUserError())
        			})
        	}
        }
        
        store.dispatch(fetchUsers())
        
        ```
        
- 

# Redux - Toolkit

### why

- Redux Requires too much Boilerplate cade
    - Action
    - Action object
    - Action creator
    - Switch statement in a reducer
    
- A lot of other package need
    - redux-thunk
    - immer
    - redux-devtools
- 

- setup
    - npm init -y
    - npm i @reduxjs/toolkit
    - index.js
    - app
        - store.js
    - features
        - cake
        - icecream
- setup cake slice
    - cakeSlice.js
        
        ```jsx
        const createSlice = require('@reduxjs/toolkit').createSlice
        
        //inital State
        const initialState = {
        	numOfCakes: 10
        }
        
        const cakeSlice = createSlice({
        	name: 'cake'
        	initialState: initialState,
        	reducers: {
        
        		// ordered is key Name for action creator 
        		ordered: (state, action) => {
        			// we do not return state
        			// we can do direact mutate state object
        			// it used immer module underhood
        			state.numOfCakes--
        		}
        		restocked: (state, action) => {
        			state.numOfCakes += action.payload
        		}
        	}
        })
        
        module.exports = cakeSlice.reducer
        module.exports.cakeActions = cakeSlice.actions
        ```
        
    - Connecting Reducer to store
        
        ```jsx
        // inside store.js
        
        const configureStore = require('@reduxjs/toolkit').configureStore
        // import reducers
        const cakeReducer = require('../features/cake/cakeSlice')
        
        const store = configureStore({
        	reducer: {
        		cake: cakeReducer,
        		icecream: icecreamReducer
        	}
        })
        
        module.exports = store
        ```
        
        ```jsx
        // index.js
        
        // import store
        const store = reqiure('./app/store')
        
        // import actions
        const cakeActions = require('./features/cake/cakeSlice').cakeActions
        
        console.log('Initial state',store.getState())
        
        const unsubscribe = store.subscribe(() => {
        	console.log('Update state ' , store.getState())
        }
        
        // Dispatching actions
        store.dispatch(cakeActions.ordered())
        store.dispatch(cakeActions.ordered())
        store.dispatch(cakeActions.ordered())
        store.dispatch(cakeActions.restocked(3))
        
        unsubscribe()
        ```
        
- apply logger middleware
    - npm i redux-logger
    
    ```jsx
    // store.js
    
    const reduxLogger = require('redux-logger')
    
    const logger = reduxLogger.createLogger()
    
    const store = configureStore({
    	reducer: {
    		cake: cakeReducer,
    		icecream: icecreamReducer
    	},
    	// getDefaultMiddleware has some default middleware
    	// we just concat our middleware over it
    	middleware: (getDefaultMiddleware) => getDefaultMiddle().concat(logger),
    })
    ```
    
- Extra Reducers
    - we want to give a free ice cream on cake order.
    - it is impossible in old redux
        - it react on action type but not able to update value of cake.
    - it is possible in redux-toolkit by using of extra-reducer
        
        ```jsx
        // ice creame slice file
        
        //....
        
        const icecreameSlice = createSlice({
        	//...
        	reducers: {
        		//...
        	},
        	extraReducers: {
        		// now it can react on action type 'cake/ordered'
        		['cake/ordered']: (state, action) => {
        			state.numberOfIcecream--
        		}
        	}
        }
        ```
        
        - Recommended way to do this is build approach
        
         
        
        ```jsx
        const {cakeActions} = require('../cake/cakeSlice')
        // ... rest code
        
        extraReducers: (builder) => {
        	// same it call called here when you ordered cake
        	builder.addCase(cakeActions.ordered, (state, action) => {
        		state.numOfIcecreams--
        	}
        }
        ```
        
- Async function in redux-toolkit
    - add userSlice file in feature
    
    ```jsx
    // userSlice
    
    const createSlice = require('@reduxjs/toolkit').createSlice
    const createAysncThunck = require('@reduxjs/toolkit').createAsyncThunk
    const axios = require('axios')
    
    const initialState = {
    	loading: false,
    	users: [],
    	error: ''
    }
    
    // Generated pending , fulfilled and rejected action type
    const fetchUsers = createAsyncThunk('user/fetchUsers', () => {
    	return axios.get('url')
    		.then( res => res.data.map(user => user.id)
    })
    
    const userSlice = createSlice({
    	name: 'user',
    	initialState,
    	extraReducers: builder => {
    		builder.addCase(fetchUsers.pending, state => {
    			state.loading = true
    		})
    
    		builder.addCase(fetchUsers.fulfilled, (state ,action) => {
    			state.loading = false,
    			state.users = actions.payload,
    			state.error = ""
    		})
    
    		builder.addCase(fetchUsers.rejected, (state ,action) => {
    			state.loading = false,
    			state.users = actions.error.message,
    			state.error = ""
    		})
    	}
    })
    
    module.exports = userSlice.reducer
    module.exports.fetchUsers = fetchUsers
    ```
    
    ```jsx
    // Store
    const userReducer = require('../features/user/userSlice')
    
    //... 
    
    reducer: {
    	cake: cakeReducer,
    	icecream: icecreamReducer,
    	user: userReducer
    }
    ```
    
    ```jsx
    // index js
    
    // import fetch api function
    	const fetchUsers = require('./features/user/userSlice').fetchUsers
    
    store.dispatch(fetchUsers)
    ```
    
- React Project Setup with redux
    - npm i axios @reduxjs/toolkit
    - app
        - store.js
        
        ```jsx
        import { configureStore } from '@reduxjs/toolkit'
        
        ...
        
        module default store
        ```
        
    - features
        - cakeSlice
            
            ```jsx
            import { createSlice } from '@reduxjs/toolkit'
            
            export default cakeSlice.reducer
            export const { ordered, restocked } = cakeSlice.actions
            ```
            
    - index.js
        
        ```jsx
        import React from 'react'
        import ReactDOM from 'react-doc'
        import { Provider } from 'react-redux'
        import store from './app/store'
        import './index.css'
        
        import App from './App'
        
        ReactDOM.render(
        	<React.StrictMode>
        		<Provider store={store}>
        			<App />
        		</Provider>
        	</React.StrictMode>, 
        	document.getElementById('rrot')
        )
        ```
        
    - App.jsx
        
        ```jsx
        import CakeView from ''
        ... 
        
           <CakeView />
        ```
        
    - views
        
        ```jsx
        import { useSelector, useDispatch } from 'react-redux'
        // Actions creators
        import { ordered, restocked } from './cakeSlice'
        
        export const CakeView = () ⇒ {
        	const numberOfCake = useSelector((state) => state.cake.numberOfCake)
        	const dispatch = useDispatch()
        	 
        	return (
        
        			<div>
        
        				<h2>Number Of cake  {numberOfCake} </h2>
        
        				<button onClick={() => dispatch(ordered)}>Order cake</button>
        
        				<button onClick={() => dispatch(restocked(5))}>Restock cakes</button>
        
        			</div>
        
        		)
        }
        
        ```
        
    - Redux Dev Tool
        - it is automatically added to redux
        - just install extension redux dev tools kit for browser
    - 
    -