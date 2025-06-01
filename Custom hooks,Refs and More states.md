# custom hooks Refs and More State 

## rules of react
hooks react me ek inbuilt function hota hai kuch kaam ko kart hai like
- Create and access states from the Fiber tree (useState)
- Register side effects in the Fiber tree (useEffect)
- Maunally select DOM selections / elements
- Many other uses

hooks hamesa use se start hote hai to ham use ke madad se khud ke custom hooks bhi bana skte hai

React comes with lots of built-in hooks:

- Most used hooks
  - useSate
  - useEffect
  - useReducer
  - useContext
- Less used hooks
  - useRef
  - useCallback
  - useTransition
  - useDeferredValue
  - useLayoutEffect
  - useDebugValue
  - useImperativeHandle
  - useId
- Library used only:
  - useSyncExternalStore
  - useInsertionEffect
 
simple rules of hooks
- always use at the top of the code
- and never call it in any nested situation , if and for
- hooks ko sirf ham recat ke function me hi bula skte hai
- Hooks are called only inside a functional component or a custom hook

## use state more ability
jaise ham abhi tak usestate me koi specific value dal pate the ab ham uske andar ek function ban kar koi kaam karwa kar jo value aye usko return karwa denge jisse ham kaam ko state ke andar hi kar lenge and jo hame usko dena hoga wah usko mil bhi jayega

example:
```jsx
const [watched , setwatched] = useState( function (){
  const datastored = localStorage.getItem("watched")
return datastored ? JSON.parse(storedvalue) : null
})

useEffect(function () {
        localStorage.setItem(watched, JSON.stringify(watched))

    }, [watched]);
```
