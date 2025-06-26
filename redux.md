# REDUX AND REDUX MODERN TOOLKIT

# basic info

- majorly redux jaha pe likha jata hai uska naam store.js/jsx hota hai
- use reducer and isme thodi bahut simlarity hoti hai
- like reducer function , intialstate

# how to intall it and use it (redux classic)?

```
npm install redux
```

then react ko use karne ke liye ham ek `createStore` ko bulate hai redux se iske madada se ham dispatch ko acces kar skte hai and current state ko bhi dekh skte hai

eg:-

```jsx
import { createStore } from "redux";

const intialstate = {
  balance: 0,
  loan: 0,
  loanpurpose: "",
};
function reducer(state = intialstate, action) {
  switch (action.type) {
    case "account/deposit":
      return { ...state, balance: action.payload + state.balance };
    case "account/withdraw":
      return { ...state, balance: action.payload - state.balance };
    default:
      return state;
  }
}

const store = createStore(reducer);
store.dispatch({ type: "account/deposit", payload: 40 });
console.log(store.getState());
```

- sabse pahle hamne import kiya hai
- and yaha pe hame stae ko intial wale state ke equal karna hota hai
- and cases kuch `first/second` order me banti hai
- then hamne createstore me reducer wale function ko diya hai jisko hamne store naam se store kiya hai
- ab is store se hi ham dispatch kar skte hai `NAME-OF-THE-STORE.dispatch(VALUE-JISKO-KARNA-HAI)`
- ab agar state ko acces karna hai to use `NAME-OF-THE-STORE.getState()` se hoga

## working with action creators

ab ham har ek kaam ke liye ek function bana denge jo hame object return kareg jisko ham bhejna chate hai

eg:-

```jsx
function deposit(amount) {
  return { type: "account/deposit", payload: amount };
}
store.dispatch(deposit(400));
console.log(store.getState());
```

## more than one reducer?

to ham do recucer ko alag alag-alag createstore se kar skte hai lekin usse jo pahle hoga use as root reducer treat kiya jayega

to is problem se bachne ke liye ham `combineReducers` ka use karte hai

```jsx
const rootReducer = combineReducers({
  stateA: firstReducer,
  stateB: secondReducer,
});
```

ye bas unke temporary naam hai bakin `:` ke baad unke real nam hai jo unke hai

for them acces

```jsx
const store = createStore(rootReducer);
```

ab isme jo bhi function dalana hai uska nam store hoga baki kam function smabhal lenge

## redux file structure slice

ab ham files ko orginise karenge

- to sabse pahle hame src me ke file bana hai `features` ke naam se
- ab aap usme apke jitne bhi reducers hai unko unke folders me dal lo
- and jo `store.jsx` wala file me bas `combinereducers` hoga jisme ham ne redcers ko bula rkha hoga and aga kisi bhi aur file me store ko acces karna ho to bas strore ko export kar lo

# contecting redux app to react

install react-redux first

```
npm install react-redux
```

then import `Provider` from recat-redux

then wrap the `<App/>` in between the `Provider`

eg:-

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { Provider } from "react-redux";
import "./index.css";
import App from "./App";

import store from "./store";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

then agar aap isko use karna chate ho to

ye ek exmaple hai jaha pe hamne kisi aur jagh ja kar store use kiya hai

```jsx
import { useSelector } from "react-redux";
function Customer() {
  const customer = useSelector((store) => store.customer);

  return <h2>👋 Welcome, {customer.fullname}</h2>;
}

export default Customer;
```

## dispatching the action from our react app

to ham action ko dispatch karte onclick ya fir onchange pe jaha pe ham unke function me values ko dispatch karwa te hai

```jsx
import { useDispatch } from "react-redux";
import { createcustomer } from "./customerSlice";
// more code
const dispatch = useDispatch();

function handleClick() {
  if (!fullName || !nationalId) return;
  dispatch(createcustomer(fullName, nationalId));
}
// more code
```

# using modern redux-toolkit(RTK)

- ye modern hai and easy hai then clasic one
- ham dono ka use same time pe kar skte hai
- ham kam code me same kam kar leneg jo ham clasic wale me kar rahe the
- ham direct hi mutates kar skte hai state me (game changer)

## creating store with RTK

To use this toolkit, first we need to install the package using the command below:

```
npm install @reduxjs/toolkit
```

then ham clasic wale trike ki jagah nay e tarike se karenge

```jsx
// store.js file hai ye
import { configureStore } from "@reduxjs/toolkit";

import accountreducer from "./features/accounts/accountslice";
import customerreducer from "./features/customer/customerSlice";

const store = configureStore({
  reducer: {
    account: accountreducer,
    customer: customerreducer,
  },
});

export default store;
```

ab ham dekhnge kaise naye tarike se ham slice kar skte hai

```jsx
// file features/featureA/domainASlice.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  state_01: 0,
  state_02: '',
};

const stateASlice = createSlice({
  name: 'stateA',
  initialState,
  reducers: {
    changeState_01(state, action) {
      state.state_01 = action.payload;
    },
    changeState_02(state, action) {
      state.state_02 = action.payload;
    },
    changeState_01_02: {
      prepare(newValue01, newValue02) {
        return {
          payload: {newValue01, newValue02},
        };
      },
      reducer(state, action) {
        state.state_01 = action.payload.newValue01;
        state.state_02 = action.payload.newValue02;
      };
    };
  };
});

export const { changeState_01, changeState_02, changeState_01_02 } = stateASlice.actions;
export default stateASlice.reducer;
```

# Context API + useReducer vs Redux Comparison

| Feature                          | Context API + useReducer                                                                                 | Redux                                                 |
| -------------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| **Bundle Size**                  | Built into React                                                                                         | Requires additional packages (larger bundle size)     |
| **Setup Complexity**             | Easy to setup a single context                                                                           | More work to setup initially                          |
| **State Management Scalability** | Additional state "slice" requires a new context setup from scratch (may cause "provider hell" in App.js) | Once set up, easy to create additional state "slices" |
| **Async Operations**             | No built-in mechanism                                                                                    | Supports middlewares for async operations             |
| **Performance Optimization**     | Requires manual effort                                                                                   | Optimized out of the box                              |
| **DevTools**                     | Only relies on React DevTools                                                                            | Comes with excellent DevTools                         |

Based on the comparison above, here are some guidelines on when to use each global state management technique:

1. Use the Context API + useReducer when...
   - it's necessary to manage global state in small applications;
   - the global state shared does not change too often (color theme, preferred language, authenticated user, etc.);
   - it's necessary to solve a simple prop drilling problem;
   - it's necessary to manage state in a local sub-tree of the application (for example the compound component pattern).
2. Use Redux when...
   - it's necessary to manage global state in large applications;
   - the global state needs to be updated frequently (shpping cart, current opened tabs, complex filters or search, etc);
   - the global state is formed by a complex state with nested objects and arrays.
