# Performance tools

to ham site ki performance ko sudhar skte by optimization

1. **PREVENT WASTED RENDERS**

   - memo
   - useMemo
   - useCallback

2. **IMPROVE APP SPEED**
   - useMemo
   - useCallback
   - useTransition
3. **REDUCE BUNDLE SIZE**
   - 3rd party packages
   - code spliting and lazy loading

## Optimizing the wasted renders

### when a comopnents get render

- when its parent componets changes
- state changes
- context changes

so ham ek optimization trick ko apna skte hai jo hai ki ham jisko render nhi krwana chate hi usko as children prop dena kyuki usse waha pahle hi hi ban kar rahega and bar bar render nhi hoga

```jsx
// "slow" component before
import { useState } from "react";

function SlowComponent() {
  // If this is too slow on your maching, reduce the `length`
  const words = Array.from({ length: 1_000 }, () => "WORD");
  return (
    <ul>
      {words.map((word, i) => (
        <li key={i}>
          {i}: {word}
        </li>
      ))}
    </ul>
  );
}

export default function Test() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Slow counter?!?</h1>
      <button onClick={() => setCount((c) => c + 1)}>Increase: {count}</button>
      <SlowComponent />
    </div>
  );
}
```

```jsx
// "slow" component after
import { useState } from "react";

function SlowComponent() {
  // If this is too slow on your maching, reduce the `length`
  const words = Array.from({ length: 5_000 }, () => "WORD");
  return (
    <ul>
      {words.map((word, i) => (
        <li key={i}>
          {i}: {word}
        </li>
      ))}
    </ul>
  );
}

function Counter({ children }) {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Slow counter?!?</h1>
      <button onClick={() => setCount((c) => c + 1)}>Increase: {count}</button>
      {children}
    </div>
  );
}

export default function Test() {
  return (
    <div>
      <Counter>
        <SlowComponent />
      </Counter>
    </div>
  );
}
```

# Memoization

to ye function ko ek bar execute karta hai then usko memoery me save kar leta then jab bhi usko re render hota hai wo check karta hai arugment same ha ya diffrent agar same to no re-render and visa-verse

- memoize a **components** with **memo**
- memoize a **object** by **useMemo**
- memoize a **function** by **useCallback**

## the memo function

ye components ko re-render nhi karta hai agar usko props same rahe

- sabse pahle to usko memo in band kiya
- fir koi const me store kiya
- fir uske jagah jis const me rakha ha usko call kiya then agar usko koi prop chaiye to bhi wah de diya use

```jsx
import { memo } from "react";

// some code here

const MemoizedComponent = memo(function (props) {
  // slow component with props code here
});

function App() {
  return <MemoizedComponent props={props} />;
}

export default App;
```

## The useMemo and useCallback hooks:

dono hi ek dependecy arrays hai like a useEffect matlab agar ki sa bhi dependency change hua to wapas se render ho jayega

saf sidhe baat me bole to ye `memo` function ki trah hai bas isme ham different kinds of inputs - instead of props, the inputs are values and functions dal skte hai

kab inka usse kiya jaye?

1. jab prop koi object ya function ho
2. bar bar re render se rukne ke liye
3. infnite useEffect ko avoid karne ke liye

usememo ke karne ke liye

- phale to jo value ko bhejna hai usko usme fill kar do
- fir usko callback karo and jisko send karna hai usko return kar do
- matlab ye ek value ko store karta hai man lo agar hame kisi value ko change hoone pe iski value ko change karana hoga to ham usko variable ko depency me rakh do

```jsx
const calculatedValue = useMemo(() => {
  // Your calculation using some variables
  return a + b * c;
}, [a, b, c]); // All used variables must be in dependencies
```

---

```jsx
import { memo, useMemo, useCallback } from "react";

// some code here

// the array of dependencies works on the same way as it would work on useEffect hook,
// so passing '[]' means the useMemo hook will run only on the initial render of
// the component that depends on it.
const propObj = useMemo(() => {
  return {
    prop1: val1,
    prop2: val2,
  };
}, []);

// the array of dependencies works on the same way as it would work on useEffect hook,
// so passing '[]' means the useCallback hook will store the function during the initial render of
// the component that depends on it.
const handleCallback = useCallback((params) => {
  // do something with params
}, []);

const MemoizedComponent = memo(function (props) {
  // slow component with props code here
});

function App() {
  return <MemoizedComponent props={propObj} callBack={hadleCallback} />;
}

export default App;
```

usecallback ko kisi function ko bhejne ke liye karo well is example me hamne `handelcallback` bheja haisame ye bhi ek depency arry pe chalta hai

eg:-

```jsx
const handleClick = useCallback(() => {
  // Function using some state/props
  console.log("Current count:", count);
  doSomething(itemId);
}, [count, itemId]); // All used values must be in dependencies
```

# Bundle Size and Code Splitting:

`bundle`: jab ham site ko visit karte hai to sabse pahle wo server se isko download karta hai uske baad hi age kuch hoga hai means react chalta hai

isko webpack banat ahai eg:- vite

`bundle size` : kitna javascript likha gya hai usko hi kahte hai

`code spliting`: ye ek esa trika hai jisse hai site ke alag alag parts ko jab ham visit karte hai tab download hota hai baki nina iske pahle sara chiz download hota hai then age kuch hota hai

## How to split the bundle code (lasy loading components) :

This means that the code will be splitted on the router component, making it so that "page" loads separetedly. Note that this technique can be applied to any component, but most coders out there mase use of it on the router level.

```jsx
import { lazy, Suspense } from "react";
import Loader from "path/to/Loader";
// some code here

const Component1 = lazy(() => import("path/to/Component1"));

// some more code here

function App() {
  return (
    <Suspense fallback={<Loader />}>
      <Component1 />
    </Suspense>
  );
}
```

suspense API ye bundle ke download hone ke bich me jo iske fallback me diya jata hai wo show karta hai

> agar aap ek bar ek place ko visit kar loge website ke then apko ye fallback wala show nhi hoga becuese ye sirf downloading ke waqt hi dikhta hai and jab aap revisit karoge to wo pahle se hi dwonloaded rahega thats why

# Does and don't checklist for optimization:

| Do                                                                                 | Don't...                                                                                                                       |
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| find performance bottlenecks using the Profiler tool and visual inspection         | optimize prematurely                                                                                                           |
| fix real performance issues                                                        | optimize anything if there is nothing to optimize                                                                              |
| memoize expensive re-renders                                                       | wrap all components in memo()                                                                                                  |
| memoize expensive calculations                                                     | wrap all values in useMemo()                                                                                                   |
| optimize context if it has many consumers and states on it change too often        | wrap all functions in useCallback()                                                                                            |
| memoize context value, direct children of the context or create separated contexts | optimize context if it's not slow and does not have many consumers (one for the current value and other for the updated value) |
| implement code splitting and lazy loading for SPA routes / components              | The above can impact performance instead of improving it                                                                       |
