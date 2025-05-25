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

```javascript html
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
```
so ham yaha pe dekh skte hai ki hamne App wale fun me Header wale ko laga diya hai means ab jo bhi header me hai wo App bbi print kar skta hai

we can re use the same as many time as we can

```js
function Title() {
  return <h1>This is my title!</h1>;
}

function App() {
  return (
    <div>
      <Title />
      <Title />
      <Title />
    </div>
  );
}
```
## what is jsx

so jsx ek js ki ek extension hai jo hame css , js and react ke components ko as html use karne deti hai and ye ek block ko return karta hai jo print hota hai website pe

### Diferences between declarative and imperative programming
- jisme hame ek ek chiz batna pade use ham imperative programing kahenge usme hame step by step batana hota hai ki kya-kya karna hai
- wahi declarative me hame ye batna hota hai ki kya karna hai not how to do it

## JavaScript logic in components

to ham js ko function me us kar skte hai but return me jsx me nhi kar skte hai agar jsx me bhi karna hai to usko iske {} andar karna padega lekin kuch hi js hai jo ham yaha pe likh skte hai
```js
function Title() {
  const hour = new Date().getHours();
  const isMorning =
    hour <= 11 ? `It's ${hour}h in the morning now!` : `It's not morning.`;
  return <h1>{isMorning}</h1>;
}
```
