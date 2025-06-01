# EFFECTS AND DATA FETCHING 

to sabse pahle Ham yah dekhenge ki hamen क्या-क्या padhna hai 


## what is the Life cycle of a component 

1. **Initial Rendering (Mounting Phase)**  
   - This is the first phase when the component loads for the first time.  
   - The component renders initially when the website is opened.  
   - During this phase, it takes in the initial **props**.  

2. **Re-rendering (Updating Phase)**  
   - This happens when there is a change in the component's **state** or **props**.  
   - If the **parent component** changes, this component re-renders.  
   - It updates the UI based on new data.  

3. **Unmounting Phase**  
   - This is the final stage where the component is removed from the screen.  
   - Happens when the component is no longer needed (e.g., when moving to a different page).  
   - Any cleanup or final code runs before the component disappears.  


## how to not do data feching

### Problem with Fetching Data Directly in Component
   - If we fetch data (like from an API) **directly inside the component**, React will keep re-rendering it **non-stop**.  
   - This happens because the component updates the state, which triggers another render, creating an **infinite loop**.  
   - This makes the app slow or even crash. 

### Solution 
to avoid this issue ham log isko useeffect nam ke hook me likhte hai jisse yah unlimited re render nhi kr payega 


## Useeffect 

1. **`useEffect` ka use tab karte hain jab hume koi aisa kaam karna ho jo React ke direct control mein na ho**, jaise:  
   - API se data fetch karna  
   - DOM ko manually update karna  
   - Timer ya subscriptions handle karna  
   - Kisi external cheez ke saath interact karna  

2. **Ye sab "side effects" hote hain**, kyuki ye React ke rendering flow se bahar hote hain, isliye inhe `useEffect` mein daalte hain taki component bar-bar re-render na kare.  

Example:  
```jsx
useEffect(function () {  
   // Yahan API call, DOM change, etc. karo  
}, []); // Ek hi baar chalega
```  
so yaha pe jo [] iske andar ham jo bhi variable/prop dalenge uske change hone par ye isko re render karwayega
jaise abhi isme kuch nhi likha hai matlab ye usko kabhi re nder nhi kar wayeg 

agar hame asynchronous function chalna hai to is function ke andar ek function Bano async se the  uske bahar usko call kar lo

and ek aur baat useeffect ki ye tabhi work karta hai jabtak pura dom tree render na ho jaye uske baad hi ye chlta hai

**Simple Matlab:**  
`useEffect` = "React ke bahar ka kaam karne ka tarika" ✅


## use of asynchronous function in useeffect 

```jsx
  useEffect( function (){
    // Step 1: Normal function banayo

    function fetchData () {
      try {
        // Step 2: API call karo (fetch/axios)
        const response = await fetch('https://api.example.com/data');
        const result = await response.json();
        
        // Step 3: Data state mein set karo
        setData(result);
      } catch (error) {
        console.error("API Error:", error);
      }
    };

    // Step 4: Function call karo
    fetchData();
  }, []); // Empty dependency = sirf ek baar chalega

}
```
Ham yahan per dekh sakte hain ki humne use effect ke andar ek asynchronous function chalaya Hai Jo ek api se data lekar aa raha hai to humne usko ek to pahle Try me Rakha Hai aur ek ko catch block mein rakha hai to try mein jo bhi error aaega wahi catch wale block me chala jayega aur ham control error kar ke console me dekh skte hai