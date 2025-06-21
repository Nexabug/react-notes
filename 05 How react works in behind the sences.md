# How react works in behind the sences

## Components, Instances and Elements:
### comopnents
componets ui ka ek building blocks hai jise ham jsx me likhte hai and jo ek react ka elemt banta hai and then usko dom me covert kar ke screen pe show kart hai its like the blueprint

### instances
so jab ham function ko kisi function me call karte hai `<Hi />` ye ek trah ka intances hai jise hamne call kiya hai
har intance ka khud ke props , children , and lifecycle hoti hai

### elements
React elements are basically the conversion of the JSX written when the function React.createElement() is called in the code. They hold all the information necessary to create DOM elements, redering those DOM elements on screen.

## how rendering works overview
to sabse pahle hota yah hai ki components hote hai then unke intense vante hai then wo sabhi react ke element me change hote hai then html me dom element me change ho jate then ui show hota hai 

### how components are displayed on the screen 
to sabse pahle render trigger hota hai then wo render phase me jata hai then waha se commit phase jaha pe check hota hai ki kya kya changes hue hai and then usko final dom me laya jata hai then ui update hota hai

ab dekho render do tarike se trigger ho skta hai
1. jab website initially load hoga tab
2. jab koi state change hoga tab

jab render hota hai to sabke liye hota hai sirf ek ke liye nhi hame sirf dikhta wahi changes hai jiska State change hua rahta hai 

## Render phase 
initial phase
to render ke Samy hota hai yah hai ki components ka ek tree banta hai jo aage chal kar react element ke tree me change ho jata hai jisko ham virtual dom kahte hai

re render trigger 
ab ek naya components ka tree banta hai jisme State change hua hai and ek naya react element ka bhi tree banega then ye pahle wale se mat h kar ke dekhenge ki kya changes hua hai the  usko to render karenge hi baki uske jitne bhi childern ele hai unko bhi re render karenga because react thodi pata hai ki uske children ele change hue hai ya nhi Isliye sabko kar deta render 


## Commit phase 
so commit phase me hota yah hai ki ise jo react ke element mile hue hai ab unko ye to use nhi kar skta kyunki wo log to ab hard-core rect hai usko dom me change karne ke liye ye `react dom` ka use Karta hai jisse wo element html ke dom me change ho jate hai

react dom website ke liye hai
react native android and iOS apps ke liye hai 

## Diffing

React mein "Diffing Algorithm" ek smart technique hai jo efficiently DOM ko update karne ke liye use hoti hai. Jab bhi component ka state ya props change hota hai:

1. React naya Virtual DOM banata hai (real DOM ki light-weight copy)
2. Purane Virtual DOM se compare karta hai
3. Sirf necessary changes real DOM mein apply karte hai

### Virtual DOM Kya Hai?

- Real DOM slow hota hai
- Virtual DOM ek JavaScript representation hai
- Har state/props change pe naya Virtual DOM banta hai

### Diffing ke 3 Golden Rules:


### Rule 1: Different Root Elements? → Puri Tree Recreate Karo

Example:
```jsx
// Purana Virtual DOM
<div>
  <h1>Hello</h1>
</div>

// Naya Virtual DOM
<span>  <-- Root change ho gaya!
  <h1>Hello</h1>
</span>
```
Result: Pure <div> aur uske children replace ho jayenge

### Rule 2: Same Root Element? → Attributes/Content Update Karo

Example:
```jsx
// Purana
<div className="old" />

// Naya
<div className="new" />  <-- Sirf className update hua
```
Result: Only className change hoga, pure element re-render nahi hoga

### Rule 3: Lists mein Keys Use Karo (Sabse Important!)
--------------------------------------------------
Bina Key ke Problem:
```jsx
// Initial List
["Mango", "Banana"]

// Updated List
["Apple", "Mango", "Banana"] <-- Start mein add kiya
```
React index se compare karega:
- Index 0: Mango → Apple (Change)
- Index 1: Banana → Mango (Change)
- Index 2: New item Banana

Result: Poori list re-render hogi!

Solution: Keys ka istemal karo
```jsx
// Sahi tareeka
{fruits.map(fruit => (
  <li key={fruit.id}>{fruit.name}</li>
))}
```
Jab key denge:
- Apple (new key) → Top par insert hoga
- Mango & Banana (existing keys) → Reuse ho jayenge

Real Code Example:
```jsx
import { useState } from 'react';

function FruitList() {
  const [fruits, setFruits] = useState(['Mango', 'Banana']);
  
  const addApple = () => {
    setFruits(['Apple', ...fruits]); // Start mein Apple add karo
  };

  return (
    <div>
      <button onClick={addApple}>Add Apple</button>
      <ul>
        {fruits.map((fruit, index) => (
          // ⚠️ Index as key (ideal nahi hai par chalta hai)
          <li key={index}>{fruit}</li>
        ))}
      </ul>
    </div>
  );
}
```
### Best Practices:

1. Keys hamesha unique dena (database ID jaise)
2. Index as key avoid karo agar list modify (add/remove) ho rahi ho
3. Complex UI ko chhote components mein tod do
4. PureComponent/React.memo use karo unnecessary re-renders rokne ke liye

### Diffing Process Steps:

1. State/Props change → Naya Virtual DOM banao
2. Purane vs naye Virtual DOM ko compare karo (Diffing)
3. Real DOM ko bataye: "Sirf in points par change karo"
4. Minimal updates → Fast UI! ⚡

### Conclusion:

React ka diffing algorithm isliye powerful hai kyunki ye minimal DOM operations karta hai. Agar aap keys ka sahi istemal karenge to apki apps ki performance bahut improve hogi!


## Library vs Framework

### frameworks 
pros
- So frameworks ek full kit hota hai jisse ham ek full stack web ko bana skte hai 
- we don't need to include any extra library for buliding a site

cons 
- hame uska convention pasand aye ya na aye hame fir bhi use use karna hi padega 
- koi bhi changes nhi kar skte hai

### library 
pros
- isme ham apne pasand ke anusar external libraryies ko laga skte hai
- variety of options to include in our project 

cons
- hame khud se unko upto date karna padta hai
- hame khud dhundh dhund kar lagana hota hai jo jyadaa time consuming bhi ho skta hai
