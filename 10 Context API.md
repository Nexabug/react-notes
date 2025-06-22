# Context API

context api solution hai `prop driling` ka jisme hame ki prop ko ek componets se dusre me pass nhi karna padta hai direct hi ham usko kahi pe bhej skte hai iski madada se

context api 3 parts me batya ja skta hai

1. **Provider** : to child componets ko sabhi value ka excces deta hai jo usko diya jata hai majorly ham isko sabse top me lagte hai becuse wha se sabko diya ja skta hai
2. **Value** : wah data jo ham pass karte hai child components me eg:- state , function etc
3. **Consumer** : to ye wo child components hai jo provier se di gyi values ko use karenge

> IMP note :- agar kisi bhi value me change hua to us value ko jis jis components ne subcribe kar rakha hai un sab me change aa jayega

# Creating and Providing Context

to sabse pahle to hame creatContext ko import karna hai then kisi const ko de dena hai

```jsx
import { createcontext } from "react";

// the variable has is decalred like that because it will return a "component"
// and as we know, components are declared with initial capital letter
const MyContext = createContext();
```

ab jab ye ban gya hai to bas hame ab isko kisi provider me rakhna hai

```jsx
// some code here...
<MyContext.Provider
  value={{
    prop1: value_prop1,
    prop2: value_prop2,
  }}
>
  <Component1 />
  <Component2 />
</MyContext.Provider>
```

ab agar hame isme se value ko consume karna hai to

```jsx
// Component1.js

import { useContext } from "react";

function Component1() {
  const { prop1 } = useContext(MyContext);

  return <div>{prop1}</div>;
}

// some more code here
```

well ham iska use aur bhi acche se kar skte hai by making custom hooks and compontes ko asn a children prop lena

```jsx
// MyContext.js
import {createContext, useContext, useState} from 'react';

const ContextComponent = createContext();

function MyContext ({children}) {
  const [val1, setVal1] = useState('My value 1');
  const [val2, setVal2] = useState([1, 2, 3]);

  function handleLogVal() {
    console.log({val1, val2})
  }

  return
    <ContextComponent.Provider
      value= {
        val1,
        val2,
        handleLogVal
      }
    >
      {children}
    </ContextComponent.Provid>
}

function useMyContext() {
  const context = useContext(ContextComponent)
  // prevents the use of the context outside the scope on which it was defined
  if (context === undefined) throw new Error ("Context used out of scope...")
  return context
}

export {MyContext, useMyContext}
```

```jsx
// App.js

// react imports ...
import { MyContext, useMyContext } from "path/to/MyContext";

// some code here
function App() {
  return (
    <>
      <Component1 />
      <MyContext>
        <Component2 />
      </MyContext>
    </>
  );
}

// some code here and definition of other compoments which do not use the imported context

function Component2() {
  const { val1, val2, handleLogVal } = useMyContext();

  // do something with the de-structured values from the imported context.
}

// some more code here
```

# Context API vs State Management

States can be classified into terms of accessibility or domain.

- Acesssiblity:
  - Local state: needed and accessible by one or few components
  - Global state: needed by many components and it's accessible to all components in the application
- Domain - Remote state: application data from a remote server (API) usually is asynchrownous because they may need refetching and updating by the use of some specialized tools - UI state: everything else, like for example, theme, filters, form data, etc - usually synchronous and stored in the application, being easy to manage because this do not interact with any server

## State placement options:

<table>
  <tr>
    <th></th>
    <th>Tools Used</th>
    <th>When to Use</th>
  </tr>
  <tr>
    <td><strong>Local Component</strong></td>
    <td>useState, useReducer or useRef</td>
    <td>Local state</td>
  </tr>
  <tr>
    <td><strong>Parent Component</strong></td>
    <td>useState, useReducer or useRef</td>
    <td>Lifting up state</td>
  </tr>
  <tr>
    <td><strong>Context</strong></td>
    <td>Context API + useState or useReducer</td>
    <td>Global state (preferably UI state)</td>
  </tr>
  <tr>
    <td><strong>3rd-party Libs</strong></td>
    <td>Redux, React Query, SWR</td>
    <td>Global state (remote or UI)</td>
  </tr>
  <tr>
    <td><strong>URL</strong></td>
    <td>React Router</td>
    <td>Global state, passing between pages</td>
  </tr>
  <tr>
    <td><strong>Browser</strong></td>
    <td>Local storage, session storage</td>
    <td>Storing data on user browser</td>
  </tr>
</table>
To sumarize, the best tools to manage all the possible types of state are:

1. Local + UI state:
   - useState, useReducer, useRef
2. Local + Remote state:
   - fetch + useEffect + useState/useReducer (used on small application)
3. Global + UI state:
   - Context API + useState/useReducer
   - Redux, Zustand, Recoil
   - React Router
4. Global + Remote state:
   - Context API + useState/useReducer
   - Redux, Zustand, Recoil
   - React Query
   - SWR
   - RTK Query
