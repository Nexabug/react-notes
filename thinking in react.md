# Thinking in react 

so isme ham log padhne 
- how to do react thinking?

## how to do react thinking?

- to sabse pahle hame kisi bhi project ko bana hai to uske pure ui ka component tree bana lo 
- ab jo components ka tree banya hai usko staticlay Bano means bina kis state ke Bano 
- ab usme state ko lagao jaha jaha pe uski jarurat 
- ab use ui se synchronous karo

## state changing and lifting up

so agar hame kabhi kisi components ki sate ko dusre ke sath share karna ho to un dono ke closet parent element me us sate ko define kar do then waha pe un dolo ko jo jo chahiye wo wo de dedo as object then unke apne function me ja kar destruction kar do us object ko unke parameter me 

is trike se ham use kar skte hai 

```jsx
function Child1({ onSetMessage }) {
  handleSetMessage('John');
}

function Child2({ msg }) {
  return <p>{msg}</p>;
}

function Parent() {
  const [msg, setMsg] = useState('');
  function handleSetMsg(name) {
    setMsg(`Hello ${name}`);
  }
  return (
    <>
      <Child1 onSetMessage={handleSetMsg} />
      <Child2 msg={msg} />
    </>
  );
}
```

so yaha pe ham `child2` me handle message me john set Kiya hai jisse msg me ab ek nya value aa gya jo john hai and usko excess `child1` bhi kar pa Raha hai 