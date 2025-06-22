# React Router

---

# making the react project by the help of vite

step 01

```
npm create vite@latest
```

step 02
name the project and also select the react with javascript now you are ready to go

step 03

```
npm install
```

step 04

```
npm run dev
```

now your is deploy on the localhost

# Routing and single page application

## what is routing?

routing ek esa process hota hai jisse ham alag alag url pe alag alag view ko show karte hai isko ham routes bolte hai example:- **www.hello.com/** , **www.hello.com/login** etc..

## single page app

- ye aise site hote hai jaha pe bina hi refresh ke sab chiz ho jata hai
- url change hone pe DOM bhi change ho jata hai
- feels like dekstop app

# implementing routing in main and other pages

> important note hame isko hamesa jo app.jsx wale me hi lagana hai

> hame ab se src wale folder me ek pages and components naam ke bhi folder bana lene hai

pages wale me sabhi pages ka inteface rahega wahi compontes me unke parts and ha har ke liye alag se ek css bhi bana lena hai chahe wo pages ho ya components

first intall react router

```
npm i react-router-dom@latest
```

yaha pe ham dekh skte hai ki hamre pass 2 pages hai ek `pagenotfound` aur ek `hompage`

pahle hamne `browserrouter` aur `routes` ko mangya

then main jo kaam hai wo ham `route` me kar rahe hai waha pe hamne pahle to usko path diya hai ki kis path pe tumhe kya kaya dikhna `element` ke andar jo components hai usko hi hame dikhana hai

agar path \* hai iska matlab diye gye path ke alwa koi bhi path pe ye dikhana hai usally ham waha pe `pagenotfound` ko dete hai

```jsx
import { BrowserRouter, Route, Routes } from "react-router-dom";
import HomePage from "path/to/HomePage";
import Component1 from "path/to/Component1";
import Component2 from "path/to/Component2";
import PageNotFound from "path/to/PageNotFound";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="relave/path1/from/root" element={<Component1 />} />
        <Route path="relave/path2/from/root" element={<Component2 />} />

        <Route path="*" element={<PageNotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

# linking between routes with `navlink` and `link`

**link** and **navlink** ye ek trah ke anchor ki trah hote hai and ye bina site ko reload kiye ek se dusre rout pe chale jate hai

in dono me ek hi diffrence hai wo diflens yah hai ki navlink ko ek class milta hai name of `active` jo clicked link ke liye hota hai wahi **link** ko yah nhi milta hai

and isko ham kuch is parkar se likhte hai

```jsx
<Link to='/PATH'>NAME-OF-THE-PATH</Link>
<NavLink to='/PATH'>NAME-OF-THE-PATH</NavLink>
```

dekhiye yaha pe ho yah raha hai ki jaise hi ham ispe click kar rahe hai ye site ko '/path' par jayega and is path pe jo bhi element ho wo hame show hoga

# STYLING OPTIONS FOR REACT APP

- Inline css
- global css file
- css module
- tailwind css

## css module

isme hai har ek chiz ke liye alag alag css file bante hai jisse kabhi problem nhi ata hai

so basicliy hame karna yah rahta hai ki jo css file ka name hota hai usko is trah se likhte hai

hamko iske andar css ko class ke rup me likhna hota hai naki html tags ko direct

```css
NAME-OF-THE-FILE.module.css
```

and then isko ham us sepecific file me import karte hai as `styles`

```jsx
import styles from "./path-of-that-module";
```

and jo bhi class se banya hai usko implement karne ke liye _className={**styles.NAME-OF-THE-CLASS**}_

is trah se use karna hai unko

agar man lo apne koi module me css class hai jisko app global ki trah banan chahte ho to uske liye app
usko kar skte ho like that

```css
:global(.Name){css propertes}
```

# nested routes and index route

nested routes matlab route ke andar route

```jsx
xyz.com; // ye homepage hai
xyz.com / path1; // ye ek route hai is site ke andar
xyz.com / path1 / path2; // ab dekho yah hai ek nested route jo route ke nadar ek aur hai
```

lets see kaise karte hai isko

dekho yaha index ko hamne jo diya hai wah hame dikahaya jayega jab ham uske parent wale ko visit karenge

ab jab hamne inko set kar diya hai next kam hara rahega ki ham ab link wale ko bhi set kar de in path pe taki wo yaha pe aa sake

> ek important note yah ki hame nested routes pe agar jana hai to link ke path me `/` se na likhe direct hi likhe

```jsx
<Route path="path/to/parent/component" element={<ParentComponent />}>
  {/* defines the index route, aka the default children element to be rendered */}
  <Route index={<DefaultChildElement />} />
  <Route
    path="path/to/child1/component/relative/to/parent"
    element={<Child1Component />}
  />
  <Route
    path="path/to/child2/component/relative/to/parent"
    element={<Child2Component />}
  />
</Route>
```

ab hamne isko jaha pe render karwana hai us components me ja kar yah likh do

```jsx
<Outlet />
```

# storing state in the URL

ham url me bhi state ko store kar skte hai iska fayda yah rahega ki ham kisi specific chizo ko share kar skte hai

www.example.com/app/cities/delhi?lat=24&lng=29

example ke liye ye site dekho

- yaha pe **/app/cities** ye path hai
- yaha pe **delhi** ek params hai
- yaha pe **lat=24&lng=29** ek query string hai

## PARAMS

agar hame params wala data lena hai to sabse pahle to hame ek route bana hoga
eg

```jsx
<Route path="cites/:ids/:car/:my" element={<Child1Component />} />
```

ab hamko agar ye value lena hai jo ids ko milega to uske liye bas ham

```jsx
example ke liye man lo site kuch esi hai
www.example.com/app/cities/india/delhi/paro
const x = useParams()
console.log(x) // ab yaha pe wo sari values jo hai parama me wo de dega kuch is trah se {ids:india , car:delhi , my:paro}
```

ham jo bhi `xyz/:__` baad likh denge wo ek ab params ban gyi hai

## query string

yaha pe ham `?` ke baad ane wali values ko lenge

```jsx
www.example.com/app/cities/delhi?lato=24&lngo=29 // man lo yah hamri site hai

// yaha pe lat aur lng do query string hai

// access the query string of the URL
const [seachParams, setSearchParams] = useSearchParams();
const stateVal1 = searchParams.get('lato');
const stateVal2 = searchParams.get('lngo');
console.log({ stateVal1, stateVal2 });

// wahi ham setSearchParams se values ko change bhi kar skte hai

setSearchParams({lato:5 , lngo:6})  // ab unki value ye ho gyi hai

```

# useNavigate

to ham isse kahi dusre jagah pe navugate karte hai

to sabse pahle usko bulao

```jsx
const navigate = useNavigate();
```

then jaha pe use karana hai waha pe use karo like me yaha pe on click pe use kara raha hu

```jsx
// react imports...
import { useNavigate } from "react-router-dom";
// other imports...

const navigate = useNavigate();

//some code here

// navigates to a specific url
<button onClick={() => navigate("new/url")}>Click me!</button>;

// navigates back in history
<button onClick={() => navigate(-1)}>Go back</button>;
```

# navigate tag

The <Navigate> component is not used anymore after the custom hook useNavigate was implement on React. Although there are some specific use cases where making use of this component can be done, and that's mostly inside nested routes, such as displayed below:

```jsx
// some code here

// the use of replace will allow to "move back" on history, if necessary
<Route element={<Navigate replace to="path/to/redirect" />} />

//some more code here
```

This component can be seen as a "redirect" component, because as soon as a specific path is reached, that will automatically "redirect" to the path specified as the to property of the <Navigate /> component.
