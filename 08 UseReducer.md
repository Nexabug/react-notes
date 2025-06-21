# UseReducer

in this lesson we will learn these topic

# what is useReducer?

yah ek Advance state Management tool hai iski madad se ham data ko store kar pate hai

```jsx
function Reducer(state, action) {}

const [count, dispatch] = useReducer(Reducer, intsialstate);
```

to yaha pe `count` value hai and `reducer` ek function hai and `intsialstate` intial value hai and jo dispatch hai uska use ham isko update karne ke liye karte hai lekin usestate ki trah nhi

REducer function me do prameter hai `state` and `action`

dekho `state` ko intial value milti hai jo usko ham dete hai wahi action update value ko dekhta hai jo usko dispatch se mila hai

ex

```jsx
function Reducer(state, action) {
  console.log(state, action); // state=> 0 ,action=> 1
}

const [count, dispatch] = useReducer(Reducer, 0);

function inc() {
  dispatch(1);
}
```

agar ham Reducer wale fun se jo bhi return karnge wo sidha count ko mil jayega kyuki count se hi ham values ko acces kar skte hai

dispatch ke andar jo bhi hota hai ham usko `action` se acces kar pate hai

`state` se hamko previso value deta hai simple bole to jo count ke pass pahle jo hota hai wo usko milta hai

well ham log dispatch ko kuch is pakar se likhte hai

logic iska yah hai ki isse ham alag alag types ke liye cases bana kar values ko return karwa skte hai

```jsx
dispatch({ type: "name", payload: "value" });
```

usereducer ka use ham isliye karte hai kyuki isse state mangement easy hota hai as compare to usestate and isse ham ek samy pe abhut sare cases ko manage kar skte hai

# usestate vs usereducer

## useState:

- Ideal for single or independent pieces of state (numbers, strings, singles arrays or object, etc.)
- The logic to update the state is places in event handlers or effects, spreading it all over one or multiple components
- Direct update states with setter functions returned from useState
- State updates are imperative
- Easy to understand and to use

## useReducer:

- Ideal for multiple related pieces of state or states with a high level of complexicity(eg., an object with multiple values or nested objects/arrays)
- The logic to update the state lives in a central place, decoupled from components, the so called reducer function
- The update of the state happens via dispatching actions to the reducer funcion, making the updates more declarative, because complex states are mapped into "well named" actions
- Can be more difficult to understand and implement

# When to use useReducer hook then?:

In order to understand when to use the useReducer hook, just answer to the questions below:

- Do my code updates just a piece of state?
- Do my states frequently update together?
- Do mu code have 3 or more pieces of related states, including objects?
- There are too many event handlers to make the components large and confusing?

`useState` should remain always the default choice for state management, but if by answering those questions or writing your code you find any issues in state managment, useReducer is the way to go.

