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