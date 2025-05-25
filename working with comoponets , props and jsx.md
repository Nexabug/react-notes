# Working with Components, Props, and JSX in React

This guide covers the essentials of React components, JSX syntax, props, rendering strategies, and more.

---

## Table of Contents

- [How to Render Anything](#how-to-render-anything)
- [Components as Building Blocks](#components-as-building-blocks)
- [What is JSX?](#what-is-jsx)
- [Creating Components](#creating-components)
- [JavaScript Logic in Components](#javascript-logic-in-components)
- [Styling in React](#styling-in-react)
- [Passing and Receiving Props](#passing-and-receiving-props)
- [Rules of JSX](#rules-of-jsx)
- [Rendering Lists](#rendering-lists)
- [Conditional Rendering](#conditional-rendering)
- [Destructuring Props](#destructuring-props)
- [Setting Classes and Text Conditionally](#setting-classes-and-text-conditionally)

---

## How to Render Anything

Start by cleaning up your React app to just two files: `app.js` and `index.js`.

In `app.js`, define your main component (component names must start with a capital letter):

```jsx
export default function App() {
  return <h1>Hello World</h1>;
}
```

The tag in the return statement will be rendered on the website.

---

## Components as Building Blocks

- React is built from components.
- Each component manages its own logic, data, and appearance.
- Components can be reused and composed.

---

## Creating Components

You can compose components by creating them separately and importing them into the main (App) component.

A function can only return one element. To return multiple, wrap them in a `<div>` or React fragment.

```jsx
export default function App() {
  return (
    <div>
      <h1>Hello World</h1>
      <Header />
    </div>
  );
}

function Header() {
  return (
    <header className="header">
      <h1>Fast React Pizza Co.</h1>
    </header>
  );
}
```

Components can be reused:

```jsx
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

---

## What is JSX?

JSX is a JavaScript extension that looks like HTML, allowing us to use CSS, JS, and React components in the same syntax. It gets compiled to JavaScript and rendered on the web page.

---

## Declarative vs. Imperative Programming

- **Imperative:** Specify _how_ to do things step by step.
- **Declarative:** Specify _what_ you want to do, not how.

---

## JavaScript Logic in Components

Use JavaScript in the function body, but not directly in the JSX. To use JavaScript in JSX, wrap it in `{}`.

```jsx
function Title() {
  const hour = new Date().getHours();
  const isMorning = hour <= 11
    ? `It's ${hour}h in the morning now!`
    : `It's not morning.`;
  return <h1>{isMorning}</h1>;
}
```

---

## Styling in React

**Inline styles:**

```jsx
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

**Directly in the element:**

```jsx
function Title() {
  return (
    <h1 style={{
      color: 'red',
      fontSize: '48px',
      textTransform: 'uppercase',
      textAlign: 'center',
    }}>
      My title
    </h1>
  );
}
```

**External CSS:**

```jsx
import './styles.css';

function Title() {
  return <h1 className="title">My Title</h1>;
}
```

---

## Passing and Receiving Props

Props are data passed from parent to child components.

```jsx
function Title(props) {
  return <h1>{props.text}</h1>;
}

function App() {
  return <Title text="Hello world!" />;
}
```

You can pass strings, arrays, objects, and even components via props.

---

## Rules of JSX

- JSX is similar to HTML, but allows using JavaScript inside `{}`.
- Inside `{}` you can use:
  - Variable references
  - Object/array creation
  - Ternary operations

You **cannot** use:
- `if/else` statements
- `for` loops
- `switch` statements

JSX must return a single element. To return multiple elements, use a wrapper `<div>` or React Fragment (`<>...</>`).

---

## Rendering Lists

Use `.map()` to render lists:

```jsx
const names = ['Maria', 'Joseph', 'Anthony'];

function Greeting(props) {
  return <h1>Hello {props.name}!</h1>;
}

function Greetings() {
  return names.map((name) => (
    <Greeting name={name} key={name} />
  ));
}
```

**Note:** Always add a unique `key` prop when rendering lists.

---

## Conditional Rendering

**Using `&&` operator:**

```jsx
function TimeOfDay() {
  const hour = new Date().getHours();
  const dayTime = 6;
  const nightTime = 18;
  const isMorning = hour >= dayTime && hour <= nightTime;
  return <div>{isMorning && <p>The sun is up!</p>}</div>;
}
```

**Using ternary operator:**

```jsx
function TimeOfDay() {
  const hour = new Date().getHours();
  const dayTime = 6;
  const nightTime = 18;
  const isMorning = hour >= dayTime && hour <= nightTime;
  return (
    <div>
      {isMorning ? <p>The sun is up!</p> : <p>It's nighttime!</p>}
    </div>
  );
}
```

---

## Destructuring Props

Instead of `props.key`, destructure in the function parameters:

```jsx
function Greeting({ name }) {
  return <h1>Hello {name}!</h1>;
}
```

Multiple props:

```jsx
function Greeting({ name, key }) {
  return (
    <>
      <h1>Hello {name}!</h1>
      <p>Bye {key}</p>
    </>
  );
}
```

---

## Setting Classes and Text Conditionally

Apply class names based on conditions:

```jsx
function Car({ carObj }) {
  return (
    <li className={`car-item ${carObj.soldOut ? 'sold-out' : ''}`}>
      <img src={carObj.photoName} alt={carObj.name} />
      <div>
        <h3>{carObj.model}</h3>
        <p>{carObj.year}</p>
        <span>{carObj.soldOut ? 'SOLD' : carObj.price}</span>
      </div>
    </li>
  );
}
```

**Explanation:**
- If `carObj.soldOut` is true, adds `'sold-out'` class.
- In the `<span>`, shows `'SOLD'` if sold out, otherwise shows the price.

---
