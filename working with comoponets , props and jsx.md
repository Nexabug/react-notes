# working with comoponets , props and jsx

so in this section ham log padhenge ki

- [how to do render any thing?]()
- [components as building blocks]()
- [what is jsx?]()
- [creating components]()
- [js logic in components]()
- [styling in react]()
- [passing and reciving the props]()
- [rules of jzx]()
- [rendering list]()
- [conditional rendering]()
- [destructring props]()
- [react fragment]()
- [setting classes and text conditionaly]()

## how to do render any thing?

to sabse pahle hamne jo react se app create Kiya hai usme se sab ko delete kar do and sirf do ko chhod do 

``` 
app.js
index.js
```
and app.js me ek app ka function Bano and ek baat yaad rahe hame jabhi koi function bana ho to uska first word hamesa capital hona chahiye otherwise it's doesn't work out

```
export default function App(){
    return(<h1> hello world </h1>)
}
```
and then return me koi bhi HTML tag dalo wo nikal kar de dega/print ho jayega website pe
so jaise ki ham yaha dekh skte hai ki hamne h1 tag lagya hai jo hello world de raha hai

## components as building blocks

- react pura hi componets se bana hai
- react karta yah hai ki wo compontes ko render karta hai
- each compontes has its own logic,data and appearance

## creating components

sabse pahle to ham alag alag components ko bante hai the usko main (App) wale function me jar kar dal dete hai

ek function sirf ek hi element ko return karta hai agar apko ek se jayada element ko karna hai return to hame un sab ko ek div me dalna padega jisse wo to ek hi element ko retun karega div but uske andar wale bhi uske sath hi return ho jayega

```javascript
export default function App(){
   
    return(
        <div>
          <h1> hello world </h1>  
           <Header/>
        </div>
        
    )
}
function Header(){
    return(
    <header className='header'><h1> fast react pizaa co.</h1></header>)
}
html```
so ham yaha pe dekh skte hai ki
