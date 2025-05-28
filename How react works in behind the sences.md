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

### assumption made by Diffing 
- do alag alag element ke tree alag alag honge
- element stable rahega agar uska koi key decide hai to otherwise nhi rahega 

to hoga yah ki man lo hamne ki ke parents ke type ko change kar diya means div se header and anything ho gya to us State me uske render hoga and  children bhi hoga render 