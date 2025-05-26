# Thinking in React

In this guide, we'll learn:
- [How to think in React](#how-to-think-in-react)
- [State changing and lifting up](#state-changing-and-lifting-up)
- [Deleting an item](#deleting-an-item)
- [Sorting of items](#sorting-of-items)
- [Children props](#children-props)

## How to think in React <a name='how-to-think-in-react'></a>

- First, when creating any project, make a component tree of the entire UI
- Build those components statically (without any state)
- Then add state wherever it's needed
- Finally, synchronize it with the UI

## State changing and lifting up <a name='state-changing-and-lifting-up'></a>

When you need to share state between components, define the state in their closest common parent component. Then pass down what each component needs as props. In their own functions, destructure these props in their parameters.

This way we can use shared state like this:

```jsx
import { useState } from "react"

export default function App(){
  const [items, setitems] = useState([])
  return (
    <div className="app">
      <Logo/>
      <Form setitems={setitems} />
      <List itemsx={items} />
      <Footer itemsx={items}/>
    </div>
  )
}

function Logo(){
  return <h1>FAR AWAY</h1>
}

function Form({setitems}){
  const [description, setDescription] = useState('')
  const [quantity, setQuantity] = useState('1')
  
  function handelSubmit(e){
    e.preventDefault()
    if(!description) return;
    const newItems = {description, quantity, packed: false, id: new Date()}
    setitems(e => [...e, newItems])
    setDescription('')
    setQuantity('1')
  }
  
  return (
    <form className="add-form" onSubmit={handelSubmit}>
      <h3>What do you need for your travel?</h3>
      <select value={quantity} onChange={(e)=>setQuantity(Number(e.target.value))}>
        <option value={1}>1</option>
        <option value={2}>2</option>
        <option value={3}>3</option>
        <option value={4}>4</option>
      </select>
      <input type='text' placeholder="Items..." value={description} onChange={(e)=>setDescription(e.target.value)}/>
      <button>Add</button>
    </form>
  )
}

function List({itemsx}){ 
  return (
    <div className="list">
      <ul>
        {itemsx.map(items => <Items items={items} key={items.id} />)}
      </ul> 
    </div>
  )
}

function Footer({itemsx}){
  return(
    <footer className="stats">
      <em>You have {itemsx.length} items and {present}% already packed</em>
    </footer>
  )
}

function Items({items}){
  return (
    <li>
      <input type="checkbox" style={{color:'red'}} value={items.packed}/>
      <span style={items.packed ? {textDecoration:'line-through'} : {}}>
        {items.quantity} {items.description}
      </span>
      <button style={{color:'red'}}>×</button>
    </li>
  )
}```

Here we can see that we created a state in the App component which is being used in List, Footer, and Form components.

## Deleting ans item <a name='deleting-an-item'></a>

Here we'll delete an item when clicking a button:
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
Here we can see that when we click the button in the Items component, the handeldelete function runs which filters out the item whose ID matches then clicked item whose will get match id but in condition we want just opposite of that means clicked item will deleted from the items array.

## sorting <a name='sorting-of-items'></a>
Here we'll sort items based on three conditions:

We'll create a new array called sorteditems which will contain the sorted version of our items array. This way, when rendering the list, we'll just use this pre-sorted array.

1. According to input order:

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
2. According to alphabetical order:
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
3. According to packed status:
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
We've written all this in the List component function because that's where we send the items array for rendering.

## Children props <a name='children-props'></a>

Now we can put content between the opening and closing tags:

```jsx
<Component></Component>
```
This way we can access the JSX between childeren element directly by putting the children prop in the child element's function, like this:
```jsx
function App() {
  return <Component>Some content between tags</Component>;
}

function Component({ children }) {
  return <div>{children}</div>;
}
```
To sumarize:

- Children props allow us to pass any JSX markup into an element
- This tool is used to make REAL en CONFIGURABLE components, allowing ease edit of their content without the need of aditional props
- This allow us to create generic components where no content was defined previously their use, as for example, components such as modals, buttons, etc.
