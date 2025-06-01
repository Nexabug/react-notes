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
const [host , setHost] = useState( function (){
  const datastored = localStorage.getItem("watched")
return datastored ? JSON.parse(storedvalue) : null
})

useEffect(function () {
        localStorage.setItem(watched, JSON.stringify(host))

    }, [host]);
```

We created a state with an initial value called `host` and its updater function `setHost`. We made a variable `dataStore` that gets an item named "watched" from local storage. Then we check `dataStore` - if it exists, we return it in parse form else, return `null`.  

We also used a `useEffect` hook that creates a local storage item named "watched". Whenever the `host` state changes, it stringifies the data and updates local storage. This keeps the stored data in sync with our state changes

## useRef
to use bhi matlab ek use State ke tarah hota hai yah bhi value store Karta Hai vah bhi value store Karta but problem nahi hai ki Jaise Ham use State kya hota tha ki jab jab uski value update hoti Thi tab tab vah render karvata tha vahi hamare pass dusre render nahin karvata jab tak Ham khud Se red internet 

Ham iske value ko badal nahin sakte Hain ki ine mutabil hota Hai

## useRef to select DOM elements 


Hum **DOM selection** ke bina bhi **DOM element** ko access kar sakte hain. Iske liye:  

1. Sabse pehle, ek **variable** banayenge jisme `useRef` ka istemal karenge.  
2. Us `variable` ka naam, jis element ko select karna hai, uske `ref` attribute mein `{variable}` daal denge.  
3. Ab dono **interconnected** ho jayenge.  
4. Agar hume us element ko access karna hai, toh `variable.current` use karenge—yeh hume woh element de dega jisse `ref` connect hai.  

example:
```jsx
const inputel = useRef(null)

  useEffect(function () {
    console.log(inputel.current) // yaha pe wah elemnt mil jayega
    inputel.current.focus() // yaha pe uspe hamne focus lagya hai
  }, [])

  return (
    <input
      ref={inputel}
    />
  )
```
to jaise ham yaha pe dekh skte hamne ek input me conect kiya hai and usme .focus nam ka effect lagya hai bina use manually DOM selection
