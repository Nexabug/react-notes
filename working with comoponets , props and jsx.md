# working with comoponets , props and jsx

so in this section ham log padhenge ki

- [how to do render any thing?]()
- [components as building blocks]()
- [what is jsx?]()
- [creating components]()
- [js logic in components]()
- [styling in react]()
- [passing and reciving the props]()
- [rules of jsx]()
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
## styling in react
so ham jsx ke element me style ko inline ki trah se laga skte hai
```js
function Title() {
  const styles = {
    color: 'red',
    fontSize: '48px',
    textTransform: 'uppercase',
    textAlign: 'center',
  };
  return <h1 style={styles}>My title</h1>;
}
```
yah fir ham direct hi us element me laga skte hai
```js
function Title() {
 
  return <h1 style={ {
    color: 'red',
    fontSize: '48px',
    textTransform: 'uppercase',
    textAlign: 'center',
  }}>My title</h1>;
}
```
agar hame external css ko lagana hai to sabse pahle to usko hame import kar lena hai then hame element ko ek `className` de skte hai jo us pe css hoga wah is pe bhi lag jayega
```js
// react imports here...
import 'path/to/css/file';

function Title() {
  return <h1 className='class-inside-css'>My Title</h1>;
}

function App() {
  <Title />;
}
```
## passing and reciving the props

props ek tarika hai jisse ham dta to parent ele se child ele me bhejte hai

iske maddad se ham child ele ko kuch data ya properties bhi de skte hai

### how to use it 

 - sabse pahle to ham jaha pe child ele ko parent me dala hai wahi pe ek atribute me koi `key="value"` se deife kar do then
 - child ele wale function me `props` naam ka ka ek parameter dal do and then jaha pe bhi us value ko acess karan ahai waha pe { } iske andr ye example hai --> `{props.key}` se bula lo yaha pe key wo name  hoga jo hane wha pe lagya tha

```js
function Title(props) {
  return <h1>{props.text}</h1>;
}

function App() {
  <Title text='Hello world!' />;
}
```
we can pass anything from the props like string , arry , object and other react container also

## rules of jsx
- jsx html ki hi trah kaam karta hai lekin isme ham javascript ko `{ }` ke ander kar skte hai
- `{ }` iske andar khuch bhi kar skte hai like variable referencing, object/array creation, ternary operations
- lekin ham kabhi bhi `if/else`  , `for` , `switch` statemnt ka use nhi kar skte hai iske andar
- jsx hame ek javascript ka expression deta hai
- agar hame return ke samy ham yah chte hai ki wo ek se jyada element bheje lenkin bina kisi div ke andar the use `<>` and `</>` for opening and closing jisse wo khud ke element me hi jayenge naki kis dusre div me

## rendering list
  to ham rendering ke liye ham ek data ko bas ek components se dusre me bhjna hota hai taki wo ja kar usse print kar de

  to isko karne ke liye ham `.map()` method se kar skte hai jisme hoga yahi ki
  - pahle to ham kisi arry pe isse use karenge
  - then usme se har ek element ko nikalenge then use child wale function ke name me denge `<nameofthechildfunction />`
  - isse hoga yah ki map jo bhi value arr se nikal kar layega use wo child function ko as a prop dega jise ham kisi `key="value"` me store kara lenge
  - then child wale function me ja kar props parameter dal kar jo bhi value hoga use le lenge
  - and hame ek key naam ki object bhi bana kar use koi unqie value de dena usse react hame koi error show nhi karega

  ```js
  const names = ['Maria', 'Joseph', 'Anthony'];

function Greeting(props) {
  return <h1>Hello {props.name}!</h1>;
}

function Greetings() {
  return names.map((el) => {
    return <Greeting name={el} key={el} />;
  });
}
```
## conditional rendering
yaha pe ham kuch condtion ke hisab se hisab se jsx ko run karwate hai means gar wo condition satisfy karega then wo jsx ko print karene dega othre wise nhi ya to kuch aur print hoga

### there are two type pf conditional rendering we can do
- `&&` conditional rendering

so isme hoga yah ki ham `&&` ke left side ek condition hogi and right side wo jsx code jisse print karwana hoga agar left wali condition true hogi tabhi agar true nhi hua to kuch bhi nhi print hoga kyuki jsx me `true` and `false` ki koi value nhi hoti hai matlab wo kabhi print nhi hote hai

```js
function TimeOfDay() {
  const hour = new Date().getHours();
  const dayTime = 6;
  const nightTime = 18;
  const isMorning = hour >= dayTime && hour <= nightTime;
  return <div>{isMorning && <p>The sun is up!</p>}</div>;
}
```
- Using `ternaries` (allows providing an alternative rendering)

so ab hoga yah ki pahle wo condtion check karega agar wo true ho gyi ti pahle jsx print hoga otherwise second jo `:` ke baad hoga agar hame chate hai ki kuch bhi print na ho to ham `''` empty ya `null` likh skte hai second wale me
```js
function TimeOfDay() {
  const hour = new Date().getHours();
  const dayTime = 6;
  const nightTime = 18;
  const isMorning = hour >= dayTime && hour <= nightTime;
  return (
    <div>{isMorning ? <p>The sun is up!</p> : <p>It's nighttime!</p>} </div>
  );
}
```
## destructring props
ab ham jo child wale function me props likhte hai use replace kar ke direct access kar skte hai bina kisi props ke bas usko hame child wale function ke para meter me destructring karna hoga us key ke naam se

```js
 const names = ['Maria', 'Joseph', 'Anthony'];

function Greeting({name}) {
  return <h1>Hello {name}!</h1>;
}

function Greetings() {
  return names.map((el) => {
    return <Greeting name={el} key={el} />;
  });
}
```
agar apko ek se jayada ko access karna hai to wahi pe comma laga kr jo uska naam hai wo likh do the usko bhi kar paoge 
```js
 const names = ['Maria', 'Joseph', 'Anthony'];

function Greeting({name , key}) {
  return <>
<h1>Hello {name}!</h1>
<p>bye {key}</p>
</>;
}

function Greetings() {
  return names.map((el) => {
    return <Greeting name={el} key={el} />;
  });
}
```
