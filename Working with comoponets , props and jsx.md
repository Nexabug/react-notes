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

First, delete everything from your src file except these two files: `app.js` and `index.js`.

In `app.js`, create an App function (remember component names must start with capital letter):

```jsx
export default function App() {
  return <h1>Hello World</h1>;
}
```

The HTML tag in the return statement will be rendered/printed on the website.

---

## Components as Building Blocks

- React is built from components.
- React renders components
- Each component manages its own logic, data, and appearance.
- Components can be reused and composed.

---

## Creating Components

First we create separate components and then import them into the main (App) component.

A function can only return one element. If you need to return multiple elements, you must wrap them in a div so they become a single element.

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
Here we can see we've included the Header component in App, so whatever is in Header will be rendered by App.

We can reuse the same component multiple times:

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

### Differences between declarative and imperative programming

- **Imperative:** requires us to specify each step of how to do something
- **Declarative:** only requires us to specify what to do, not how to do it

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

**We can apply inline styles to JSX elements:**

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

**Or directly in the element:**

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

**For external CSS, first import the CSS file, then use `className`:**

```jsx
import './styles.css';

function Title() {
  return <h1 className="title">My Title</h1>;
}
```

---

## Passing and Receiving Props

Props are used to pass data from parent to child components.

### How to use props
- Add attributes to the child component in the parent: `<Child key="value" />`
- In the child component, accept `props` as a parameter
- Access the value using `{props.key}`

```jsx
function Title(props) {
  return <h1>{props.text}</h1>;
}

function App() {
  return <Title text="Hello world!" />;
}
```

We can pass strings, arrays, objects, and even components via props.

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

To render lists, we pass data from parent to child components using the .map() method:

- Use .map() on an array
- For each element, return the child component <ChildComponent />
- Pass array data as props to the child
- The child component receives props and renders them
- Add a unique key prop to avoid React errors

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


---

## Conditional Rendering

We can render JSX based on conditions.

### Two types of conditional rendering:
1. `&&` operator:
   - Left side: condition
   - Right side: JSX to render if condition is true
   - If false, nothing renders (JSX doesn't render `true/false`)

```jsx
function TimeOfDay() {
  const hour = new Date().getHours();
  const dayTime = 6;
  const nightTime = 18;
  const isMorning = hour >= dayTime && hour <= nightTime;
  return <div>{isMorning && <p>The sun is up!</p>}</div>;
}
```  
2. Ternary operator:
   - If condition is `true`, renders first JSX
   - If `false`, renders second JSX after `:`
   - Use `null` or `''` to render nothing

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

Instead of using `props.key`, we can destructure props directly in the function parameters:

```jsx
function Greeting({ name }) {
  return <h1>Hello {name}!</h1>;
}
```

For multiple props:

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

We can conditionally apply classNames:

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
