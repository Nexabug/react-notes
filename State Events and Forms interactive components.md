# State Events and Forms Interactive Components

In this section, we will cover:

- [Handling the Event in React](#handling-the-event-in-react)
- [What is State?](#what-is-state)
- [Creating a State Variable with useState](#creating-a-state-variable-with-usestate)
- [Updating State](#updating-state)
- [A Bit More About States and Some Guidelines](#a-bit-more-about-states-and-some-guidelines)
- [Forms in React](#forms-in-react)
- [State vs Props](#state-vs-props)

---

## Handling the Event in React <a name='handling-the-event-in-react'></a>

To handle events in React, we use inline event handlers written in camelCase notation instead of `addEventListener()`. Examples include `onClick`, `onMouseHover`, `onChange`, etc.

For example, here's a button that shows an alert when clicked:

```jsx
function AlertButton() {
  return <button onClick={() => alert('You clicked me!')}>Click me</button>;
}
```

If we've already defined the function separately:

```jsx
function AlertButton() {
  // The "handle" prefix in the function name follows React conventions for better code readability
  const handleAlert = () => alert('You clicked me!');
  return <button onClick={handleAlert}>Click me</button>;
}
```

---

## What is State? <a name='what-is-state'></a>

State is like a component's memory, specific to that component. We can't use it outside the component where it's defined.

Each variable that stores state value is called a `"piece of state"`. When we update any piece of state, React automatically re-renders the component, keeping the UI in sync with the state.

---

## Creating a State Variable with useState <a name='creating-a-state-variable-with-usestate'></a>

To use state, define it inside your component: `const [name, setName] = useState(initialValue)`

Here, `name` is the state variable, `setName` is the function to update it, and `initialValue` is the starting value for `name`.

When we call `setName` with a new value, the `name` variable gets updated.

Example:

```jsx
import { useState } from 'react';

function CounterButton() {
  const [count, setCount] = useState(0);
  const handleClick = () => {
    setCount(count + 1);
  };
  return <button onClick={handleClick}>You clicked me {count} times.</button>;
}
```

---

## Updating State <a name='updating-state'></a>

The best way to update state is by using a callback function. The setter function (like setCount) can accept a function that receives the current state value and returns the new value.

```jsx
function CounterButton() {
  const [count, setCount] = useState(0);
  const handleClick = () => {
    setCount((currCount) => currCount + 1);
  };
  return <button onClick={handleClick}>You clicked me {count} times.</button>;
}
```

---

## A Bit More About States and Some Guidelines <a name='a-bit-more-about-states-and-some-guidelines'></a>

- Each component manages its own state, no matter how many times it's rendered in the UI
- The UI is essentially a reflection of states and props
- State should only be used for values that change due to user interactions, not just for storing any value

---

## Forms in React <a name='forms-in-react'></a>

To create a form in JSX, we write it similarly to HTML:

```jsx
function MyForm() {
  return (
    <form>
      <input placeholder='Any placeholder text' />
      <input type='checkbox' />
      Just a checkbox
      <button>Submit</button>
    </form>
  );
}
```

To make the form interactive:

```jsx
function MyForm() {
  const [text, setText] = useState('');
  const handleTextChange = (e) => {
    setText(e.target.value);
  };
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(text);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input
        placeholder='Any placeholder text'
        onChange={handleTextChange}
        value={text}
        name='input'
      />
      <button>Submit</button>
    </form>
  );
}
```

In this example:

- We create a state variable `text` with an initial empty value
- The input field updates this state via the `onChange` handler
- When the form is submitted, we prevent the default behavior and log the current value

---

## State vs Props <a name='state-vs-props'></a>

**States:**
- Internal data, owned by the component
- Acts as "component memory"
- Can only be used by the component itself
- Causes a component re-render when updated
- Used to make components interactive

**Props:**
- External data, owned by a parent component
- Passed to the component like function parameters
- They are read-only (immutable)
- A component re-renders when it receives new props
- Used by parent components to configure child components
