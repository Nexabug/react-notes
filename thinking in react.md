# Thinking in react 

so isme ham log padhne 
- how to do react thinking?
- state changing and lifting up
- deleting the item
- sorting of items

## how to do react thinking?

- to sabse pahle hame kisi bhi project ko bana hai to uske pure ui ka component tree bana lo 
- ab jo components ka tree banya hai usko staticlay Bano means bina kis state ke Bano 
- ab usme state ko lagao jaha jaha pe uski jarurat 
- ab use ui se synchronous karo

## state changing and lifting up

so agar hame kabhi kisi components ki sate ko dusre ke sath share karna ho to un dono ke closet parent element me us sate ko define kar do then waha pe un dolo ko jo jo chahiye wo wo de dedo as object then unke apne function me ja kar destruction kar do us object ko unke parameter me 

is trike se ham use kar skte hai 

```jsx
import { useState } from "react"

export default function App(){
  const [items , setitems] = useState([])
  return(<div  className="app">
    <Logo/>
    <Form setitems={setitems} />
    <List itemsx={items} />
    <Footer itemsx={items}/>
  </div>)
}

function Logo(){
 return <h1> FAR AWAY</h1>
}

function Form({setitems}){
  const [description , setDescription]=useState('')
  const [quantity , setQuantity]=useState('1')
  function handelSubmit(e){
   e.preventDefault()
   if(!description) return;
   const newItems ={ description , quantity , packed:false , id:new Date()}
   setitems(e => [...e , newItems])
  setDescription('')
  setQuantity('1')
  }
  return <form className="add-form" onSubmit={handelSubmit}>
    <h3> what do you need for your travel?</h3>
    <select value={quantity} onChange={(e)=>setQuantity(Number(e.target.value))}>
      <option value={1}>1</option>
      <option value={2}>2</option>
      <option value={3}>3</option>
      <option value={4}>4</option>
    </select>
    <input type='text' placeholder="items..."  value={description} onChange={(e)=>setDescription(e.target.value)}/>
    <button>Add</button>
  </form>
}

function List({itemsx}){ 
  return (
  <div className="list">
<ul>
    {itemsx.map(items=> <Items items={items} key={items.id} />)}
    </ul> 
  </div>
)
}
function Footer({itemsx}){
  return(
    <footer className="stats">
      <em> you have {itemsx.length} items and {present}% already packed</em>
    </footer>
  )
}
function Items({items}){
 return(<li>
    <input type="checkbox" style={{color:'red'}} value={items.packed}/>
     <span style={items.packed?{textDecoration:'line-through'}:{}}>{items.quantity} {items.description}</span>
   <button style={{color:'red'}}>&times;</button> </li>)
}
```

so ham yaha pe deklh skte hai ki hamne App wale  fun me ek state banya hai jo ham list , footer and form sab me us value ko liya ja raha hai 

## deleting ans item

so isme ham ek item ko delet karenge when we click on a button
```jsx
export default function App(){
  const [items , setitems] = useState([])
function handeldelet(id){
    setitems(items => items.filter(e =>e.id !== id))
  }
  return(<div  className="app">
    <Logo/>
    <Form setitems={setitems} />
    <List itemsx={items} handeldelet={handeldelet}/>
    <Footer itemsx={items}/>
  </div>)
}

function Items({items , handeldelet}){

  return(<li>
    <input type="checkbox" style={{color:'red'}} value={items.packed}/>
     <span style={items.packed?{textDecoration:'line-through'}:{}}>{items.quantity} {items.description}</span>
   <button style={{color:'red'}} onClick={()=>handeldelet(items.id)}>&times;</button> </li>)
}

```
so ham yaha pe dekh skte hai ki jab ham items wale button ko click kar rahe hai tab handeldelete wala ek function chal raha hai jo filter kar raha hai ki jispe click hua hai uske sath kisi ka id match hua ya nhi jiska match ho jayega usee nikal dega and yaha pe wo khud ka hi match karega means khud hi bahr nikal jayega

## sorting 
so insme ham items ko 3 condition me sort karenge 

so is wale me hoga yah ki ham items ki arry ko ek ham khud ka arry sorteditems naam ke equal hoga isse hoga yah ki ham imtems ke order ko pahle hi change kar denge jisse list ko render karene ke liye bas use sortedimests wali arry ka use karna hoga jo pahle se hi sorted kiya hoga hamne 

1. accoring of input order

so yaha pe ek condition layenge agar option me `sort by input` hoga to sorteditems = hoga items ke
```jsx
const [sort , setsort] = useState('input')
let sorteditems;
  if(sort === 'input') sorteditems = itemsx
return (
  <div className="list">
     <ul>
    {sorteditems.map(items=> <Items items={items} key={items.id} handeldelet={handeldelet} handelpacked={handelpacked}/>)}
    </ul> 
    <select className="actions" value={sort} onChange={e=> setsort(e.target.value)}>
      <option value='input'>sort by input</option>
    </select>
  </div>
)
```
2. according to aplaphabatic
```jsx
 const [sort , setsort] = useState('input')
  let sorteditems;
  if(sort === 'description') sorteditems = itemsx.sort((a,b) => a.description.localeCompare(b.description))
return (
  <div className="list">
     <ul>
    {sorteditems.map(items=> <Items items={items} key={items.id} handeldelet={handeldelet} handelpacked={handelpacked}/>)}
    </ul> 
    <select className="actions" value={sort} onChange={e=> setsort(e.target.value)}>
      <option value='description'>sort by description</option>
    </select>
  </div>
)
```
3. according to packed or not?
```jsx
 const [sort , setsort] = useState('input')
  let sorteditems;
 if(sort === 'packed') sorteditems = itemsx.sort((a,b) => Number(a.packed) - Number(b.packed))
return (
  <div className="list">
     <ul>
    {sorteditems.map(items=> <Items items={items} key={items.id} handeldelet={handeldelet} handelpacked={handelpacked}/>)}
    </ul> 
    <select className="actions" value={sort} onChange={e=> setsort(e.target.value)}>
      <option value='packed'>sort by packed</option>
    </select>
  </div>
)
```

and ye sab ham ne list wale function me likha hai becuse wahi items ko arr bhejta hao render ke liye
