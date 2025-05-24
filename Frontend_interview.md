# Interview Questions and Answers: Frontend Technologies

---

## Table of Contents

- [HTML](#html)
  - [Basic](#html-basic)
  - [Intermediate](#html-intermediate)
  - [Advanced](#html-advanced)
- [CSS](#css)
  - [Basic](#css-basic)
  - [Intermediate](#css-intermediate)
  - [Advanced](#css-advanced)
- [JavaScript](#javascript)
  - [Basic](#javascript-basic)
  - [Intermediate](#javascript-intermediate)
  - [Advanced](#javascript-advanced)
  - [Practical](#javascript-practical)
- [React](#react)
  - [Basic](#react-basic)
  - [Intermediate](#react-intermediate)
  - [Advanced](#react-advanced)

---

## JavaScript

### JavaScript - Basic

**1. What is StrictMode?**  
Strict Mode (`'use strict';`) is a restricted JavaScript variant that eliminates silent errors and makes debugging easier. It prevents certain actions such as assigning to undeclared variables, and throws errors for unsafe actions.  
**Real-world example:**  
In production code, strict mode helps catch typos and prevents accidental global variable declarations.

---

**2. What are data types? How do you define variables?**  
JavaScript data types:
- **Primitive:** string, number, boolean, null, undefined, symbol, bigint  
- **Non-Primitive:** object, array, function  

Variables can be defined using `var`, `let`, or `const`:
```js
let name = "Jay";
const PI = 3.14;
var isActive = true;
```
**Best practice:**  
Use `let` and `const` for block-scoped variables.

---

**3. Primitive and Non-Primitive Data Types**  
_Primitive:_ Immutable, directly contain value (e.g., `5`, `"hello"`).  
_Non-Primitive:_ Mutable, reference type (e.g., `{}`, `[]`, functions).  
```js
let arr = [1,2,3]; let arr2 = arr; arr2.push(4); // arr is now [1,2,3,4]
```

---

**4. What is an event loop?**  
The event loop allows JavaScript to perform non-blocking operations by offloading tasks (timers, network requests) to the browser, which then schedules callbacks when the stack is empty.  
**Real-world:**  
AJAX calls don’t freeze the UI because of the event loop.

---

**5. What is Async and Await?**  
`async` and `await` are used to write promise-based asynchronous code in a synchronous style.  
```js
async function fetchData() {
  const response = await fetch('/api/data');
  const data = await response.json();
  return data;
}
```
**Real-world:**  
Fetching and displaying user data after login.

---

### JavaScript - Intermediate

**1. Features of ES5**  
- Strict mode
- Array methods (`forEach`, `map`, `filter`)
- `Object.create()`
- Getters and setters  
**Real-world:**  
Legacy browsers support ES5; many polyfills target ES5 features.

---

**2. What is a callback function?**  
A function passed as an argument to another function to be executed later.  
```js
function greet(name, cb) { cb(name); }
greet('Jay', (n) => alert(`Hello, ${n}`));
```
**Real-world:**  
Used in event handling and asynchronous operations.

---

**3. What is callback hell? How to handle it?**  
Nested callbacks make code hard to read and maintain—known as "callback hell."
**Handling:**  
- Use Promises or async/await to flatten code structure.
**Example:**  
```js
doA(() => {
  doB(() => {
    doC(() => { ... });
  });
});
// Becomes:
doA().then(doB).then(doC);
```

---

**4. What is a promise? Refer all methods related to promises.**  
A Promise represents a value that may be available now, later, or never.  
- `then`, `catch`, `finally`
- `Promise.all`, `Promise.race`, `Promise.allSettled`, `Promise.any`  
**Real-world:**  
Making multiple AJAX calls in parallel and waiting for all to finish.

---

**5. Difference between axios and fetch**  
- **fetch:** Native, promise-based, minimal configuration.
- **axios:** Third-party, supports older browsers, automatic JSON parsing, interceptors, request cancellation.
**Real-world:**  
Use axios for complex apps needing features like interceptors or timeout.

---

**6. Destructuring, Currying, and Closure**  
- **Destructuring:** Unpacks values from arrays/objects.
  ```js
  const [a, b] = [1, 2];
  const {name} = {name: 'Jay'};
  ```
- **Currying:** Transforming a function with multiple arguments into a series of functions.
  ```js
  const sum = a => b => a + b;
  ```
- **Closure:** Function retaining access to its scope after the outer function has executed.
  ```js
  function outer() { let x = 1; return () => x++; }
  ```

---

**7. Explain debounce and throttling with code**  
- **Debounce:** Delay execution until a period of inactivity.
  ```js
  function debounce(fn, delay) {
    let timer;
    return function(...args) {
      clearTimeout(timer);
      timer = setTimeout(() => fn.apply(this, args), delay);
    }
  }
  ```
- **Throttle:** Limit execution to once every given interval.
  ```js
  function throttle(fn, limit) {
    let inThrottle;
    return function(...args) {
      if (!inThrottle) {
        fn.apply(this, args);
        inThrottle = true;
        setTimeout(() => inThrottle = false, limit);
      }
    }
  }
  ```
**Real-world:**  
Debounce for search inputs, throttle for window resize events.

---

**8. Arrow functions vs Regular functions**  
- **Arrow:** Shorter syntax, lexical `this`, cannot be used as constructors.
- **Regular:** Have their own `this`, can be constructors.
**Example:**
```js
const f1 = () => this; // takes `this` from enclosing scope
function f2() { return this; } // `this` depends on how called
```
**Real-world:**  
Event handlers in React often use arrow functions to preserve `this`.

---

**9. Methods of Array and Object**  
- Array: `map`, `filter`, `reduce`, `forEach`, `find`, `includes`, `push`, etc.
- Object: `Object.keys`, `Object.values`, `Object.entries`, `hasOwnProperty`, etc.
**Real-world:**  
Using `reduce` to sum array values.

---

**10. Array methods: map, filter, reduce, and shift**  
- `map`: Creates new array by applying function to each element.
- `filter`: Creates new array with elements passing test.
- `reduce`: Reduces array to single value.
- `shift`: Removes and returns first element.
**Example:**
```js
[1,2,3].map(x => x*2); // [2,4,6]
[1,2,3].filter(x => x>1); // [2,3]
[1,2,3].reduce((a,b) => a+b, 0); // 6
[1,2,3].shift(); // 1
```

---

**11. Array and Object Destructuring Syntax**  
```js
const arr = [1,2,3]; const [a,b] = arr;
const obj = {x:1, y:2}; const {x, y} = obj;
```
**Real-world:**  
Extracting props from objects in React components.

---

### JavaScript - Advanced

**1. What are constructor functions? Why use them over normal functions/objects?**  
Constructor functions are templates for creating objects. When called with `new`, they create new instances.
```js
function Person(name) { this.name = name; }
let p = new Person('Jay');
```
**Why:**  
Supports object-oriented design, inheritance via prototypes.

---

**2. “this” keyword-related questions**  
`this` refers to the context in which a function is called.
- In a method: the object before the dot
- Alone: global (`window` in browsers)
- Arrow functions: inherit `this` from parent
**Real-world:**  
In React class components, event handlers need `this` binding.

---

**3. Copying objects and changing their values**  
- **Shallow copy:** `Object.assign({}, obj)` or spread: `{...obj}`
- **Deep copy:** `JSON.parse(JSON.stringify(obj))` (caveats with functions/symbols)
**Example:**
```js
let a = {x:1}; let b = {...a}; b.x = 2; // a.x still 1
```

---

**4. What is the call, bind, and apply method?**  
They set the value of `this` in function calls:
- `call`: `fn.call(context, arg1, arg2)`
- `apply`: `fn.apply(context, [arg1, arg2])`
- `bind`: returns new function with `this` bound
**Real-world:**  
Borrowing array methods for array-like objects.

---

**5. What is the pick function?**  
A utility to select specific properties from an object.
```js
function pick(obj, keys) {
  return keys.reduce((acc, key) => {
    if (obj[key]) acc[key] = obj[key];
    return acc;
  }, {});
}
```
**Real-world:**  
Extracting only needed fields from API response.

---

**6. Closure, IIFE, scope of function and variable, timeout with loop, quality constraint of variable**  
- **Closure:** Inner function remembers variables from outer scope.
- **IIFE:** Immediately Invoked Function Expression, used to create private scope.
- **Scope:** var (function), let/const (block).
- **Timeout with loop:** Use `let` or IIFE to capture loop variable.
```js
for(var i=0;i<3;i++) {
  setTimeout(() => console.log(i), 0); // 3 3 3
}
for(let i=0;i<3;i++) {
  setTimeout(() => console.log(i), 0); // 0 1 2
}
```

---

**7. First-class functions in JavaScript**  
Functions are treated as values; they can be assigned, returned, and passed as arguments.
**Example:**  
```js
function greet(fn) { fn(); }
greet(() => console.log('Hi'));
```
**Real-world:**  
Callbacks, event handlers.

---

### JavaScript - Practical

**1. Numeric array: How do you get the sum of the array? ([12, 2, 3, 4])**  
```js
[12, 2, 3, 4].reduce((a, b) => a + b, 0); // 21
```

---

**2. Reverse a string using reduce**  
```js
const str = "hello";
const rev = str.split('').reduce((acc, ch) => ch + acc, '');
```

---

**3. Return all values from an array where the value is <5**  
```js
[1, 6, 3, 8, 2].filter(x => x < 5); // [1,3,2]
```

---

**4. Sum of numbers in a nested array ([1, 2, 3, [4, 5], [7, [8]], 9])**  
```js
function sum(arr) {
  return arr.reduce((acc, val) =>
    Array.isArray(val) ? acc + sum(val) : acc + val, 0);
}
sum([1, 2, 3, [4, 5], [7, [8]], 9]); // 39
```

---

**5. Write a code for the myFilter function that behaves like filter.**  
```js
function myFilter(arr, fn) {
  const res = [];
  for (let el of arr) if (fn(el)) res.push(el);
  return res;
}
```

---

**6. Function currying: sum(2, 3, ...)(1, 2, ...)(4)(5)**  
```js
function sum(...args) {
  let total = args.reduce((a, b) => a + b, 0);
  function inner(...next) {
    if (next.length === 0) return total;
    total += next.reduce((a, b) => a + b, 0);
    return inner;
  }
  return inner;
}
sum(2,3)(1,2)(4)(5)(); // 17
```

---

**7. Remove duplicate objects from an array of objects:**  
```js
let arr = [
  {id: 1, name: "sam"},
  {id: 2, name: "max"},
  {id: 3, name: "steel"},
  {id: 1, name: "scott"}
];
let unique = [];
let ids = new Set();
for (let obj of arr) {
  if (!ids.has(obj.id)) {
    unique.push(obj);
    ids.add(obj.id);
  }
}
```

---

### JavaScript - Advanced (continued)

**8. What is memory leak in JS? explain real world cases and how to prevent it**  
A memory leak occurs when memory that is no longer needed is not released.  
**Examples:**  
- Unremoved event listeners.
- Forgotten closures referencing large objects.
- Global variables holding unused data.
**Prevention:**  
- Remove event listeners on cleanup.
- Nullify references when done.
**Real-world:**  
Single-page apps can leak memory if event handlers aren’t cleaned up during navigation.

---

**9. Async Programming in JavaScript**  
Handles operations like network requests without blocking the main thread.  
**Tools:** Callbacks → Promises → async/await.  
**Real-world:**  
Fetching data, UI updates, timers.

---

**10. When to use for…of vs for…in?**  
- `for...of`: Iterates over iterable values (arrays, strings).
- `for...in`: Iterates over enumerable property names (objects, arrays, but includes inherited keys).
**Example:**
```js
for (let v of [1,2,3]) { ... } // values
for (let k in {a:1,b:2}) { ... } // keys
```

---

### JavaScript - Practical (continued)

**11. [Leetcode: Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)**  
Check for balanced parentheses using a stack:
```js
function isValid(s) {
  let stack = [];
  let map = {')':'(', '}':'{', ']':'['};
  for (let ch of s) {
    if ('({['.includes(ch)) stack.push(ch);
    else if (stack.pop() !== map[ch]) return false;
  }
  return stack.length === 0;
}
```

---

**12. Find the number with least frequency**  
```js
const nums = [1,2,3,1,2,3,1,3,4,1,2,4,4,3,4,4];
const freq = {};
for (let n of nums) freq[n] = (freq[n]||0)+1;
let min = Math.min(...Object.values(freq));
Object.keys(freq).filter(k => freq[k] === min); // numbers with least freq
```

---

**13. Find the pattern and implement the function input -> jayVpatel | output -> ajVyapetl**  
```js
function pattern(str) {
  let [first, ...rest] = str;
  const idx = rest.findIndex(c => c === c.toUpperCase());
  let out = rest.slice(0, idx).concat(first, rest.slice(idx)).join('');
  return out;
}
pattern("jayVpatel"); // ajVyapetl
```

---

**14. Given the array const nums = ['1', ..., '8']; print colors in sequence.**  
```js
const nums = ['1','2','3','4','5','6','7','8'];
const colors = ['red','green','yellow'];
for (let i=0; i<nums.length; i++) {
  console.log(`Num: ${nums[i]}, Color: ${colors[i % 3]}`);
}
```

---

**15. [Leetcode: Two Sum](https://leetcode.com/problems/two-sum/description/)**  
```js
function twoSum(nums, target) {
  let map = {};
  for (let i=0; i<nums.length; i++) {
    let diff = target - nums[i];
    if (map[diff] !== undefined) return [map[diff], i];
    map[nums[i]] = i;
  }
}
```

---

**16. Implement cache mechanism using JS closures**  
```js
function createCache() {
  const cache = {};
  return function(key, val) {
    if (val !== undefined) cache[key] = val;
    return cache[key];
  }
}
const cache = createCache();
cache('a', 1); // set
cache('a'); // get
```

---

## React

### React - Basic

**1. Virtual DOM vs Real DOM**  
The Virtual DOM is a lightweight JavaScript representation of the Real DOM. React updates the Virtual DOM first, then efficiently updates only the changed parts in the Real DOM.  
**Real-world:**  
Improves UI performance for large dynamic web apps.

---

**2. What is the latest version of React and what new features were introduced?**  
As of early 2025, React 19 is the latest, introducing features like the `use` hook, better server components, improved Suspense, and startTransition API.  
**Example:**  
The `use` hook simplifies data fetching in server components.

---

**3. React and its advantages**  
- Component-based architecture  
- Reusable UI components  
- Virtual DOM for performance  
- Strong ecosystem  
**Real-world:**  
Used by Facebook, Instagram, Airbnb for scalable UIs.

---

**4. What is JSX (with full form)? How is JSX rendered on components? What is the purpose of JSX in React?**  
JSX: JavaScript XML. A syntax extension allowing HTML-like code in JS.  
JSX is transpiled to `React.createElement` calls.  
**Purpose:**  
Improves readability, enables component-based development.
```jsx
const Hello = () => <h1>Hello!</h1>;
```

---

**5. What are state and props?**  
- **State:** Local, mutable data managed by the component.
- **Props:** External, read-only data passed from parent to child.
**Example:**  
```jsx
function Child({name}) { return <p>{name}</p>; }
```

---

**6. Function-based Components**  
Components written as functions, using hooks for state and lifecycle.
```jsx
function MyComponent() { return <div>Hello</div>; }
```

---

**7. Class-based Components**  
Components using ES6 classes, managing state via `this.state` and lifecycle via methods.
```jsx
class MyComponent extends React.Component {
  render() { return <div>Hello</div>; }
}
```

---

**8. What is the difference between functional and class-based components?**  
- Functions: Simpler, use hooks, no `this`
- Classes: More verbose, use lifecycle methods, have `this`
**Real-world:**  
Modern React favors functional components.

---

**9. How do you pass data from the parent component to the child component and vice versa?**  
- Parent to child: via props.
- Child to parent: pass a callback as a prop.
```jsx
<Child onChange={val => setState(val)} />
```

---

**10. Why do we add a unique key when we use the map method?**  
Keys help React identify which items have changed, added, or removed and optimize rendering.
**Real-world:**  
List rendering in dynamic UIs.

---

**11. Router Implementation (BrowserRouter and HashRouter)**  
- **BrowserRouter:** Uses HTML5 history API for clean URLs.
- **HashRouter:** Uses hash in URL (`#/page`) for legacy support.
```jsx
import { BrowserRouter } from 'react-router-dom';
```
**Real-world:**  
SPA navigation.

---

**12. What is controlled and uncontrolled components?**  
- **Controlled:** Form data managed by React state.
- **Uncontrolled:** Form data managed by the DOM (via refs).
**Example:**  
Controlled:
```jsx
<input value={value} onChange={e => setValue(e.target.value)} />
```
Uncontrolled:
```jsx
<input ref={inputRef} />
```

---

### React - Intermediate

**1. Difference between functional and class-based components**  
*(See basic section above)*

---

**2. What are lifecycle methods in React? Share for both class-based and function-based components.**  
- **Class:** `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`
- **Function:** `useEffect` hook replaces all lifecycle methods.
```jsx
useEffect(() => { ... }, [deps]); // runs on mount/update
useEffect(() => { return () => {...} }, []); // cleanup on unmount
```

---

**3. useState and useEffect hook implementation**  
- `useState`: for state management
- `useEffect`: for side effects
```jsx
const [count, setCount] = useState(0);
useEffect(() => { document.title = count; }, [count]);
```

---

**4. Best React Practices**  
- Use functional components and hooks
- Keep components small and focused
- Use keys in lists
- Avoid side effects in render
- Use Context API or Redux for global state

---

**5. Props drilling**  
Passing data through many layers of components.  
**Solution:**  
Use Context API or state management libraries.

---

**6. Fragments**  
Allow grouping children without extra nodes:
```jsx
<>
  <ChildA />
  <ChildB />
</>
```

---

**7. Context API with Implementation**  
Context provides global state to components:
```jsx
const MyContext = React.createContext();
<MyContext.Provider value={data}>
  <Child />
</MyContext.Provider>
const value = useContext(MyContext);
```

---

**8. Custom hooks**  
Reusable logic extracted into functions starting with `use`.
```js
function useCounter() {
  const [count, setCount] = useState(0);
  ...
}
```

---

**9. Router Implementation**  
*(See basic section)*

---

**10. How to optimize a React application?**  
- Use React.memo, useCallback, useMemo
- Avoid unnecessary re-renders
- Lazy-load components
- Code splitting

---

### React - Advanced

**1. Higher Order Components**  
A function that takes a component and returns a new component.
```js
function withUser(Wrapped) { ... }
```
**Real-world:**  
Adding authentication, logging, etc.

---

**2. Middleware (thunk, saga)**  
- **Thunk:** Middleware for async logic in Redux.
- **Saga:** Middleware for complex async flows using generators.
**Real-world:**  
Managing side effects like data fetching.

---

**3. What is Lazy import?**  
Dynamically load components using React.lazy for code splitting.
```js
const LazyComp = React.lazy(() => import('./LazyComp'));
```

---

**4. How to use useEffect as a willUnmount**  
Return a cleanup function in useEffect:
```js
useEffect(() => {
  // setup
  return () => { /* cleanup */ }
}, []);
```

---

**5. Difference between useMemo and useCallback**  
- `useMemo`: Memoizes a value.
- `useCallback`: Memoizes a function.
```js
const memoVal = useMemo(() => compute(val), [val]);
const memoFn = useCallback(() => fn(val), [val]);
```

---

**6. How to avoid re-rendering in functional components**  
- Use React.memo, useCallback, useMemo
- Proper key usage in lists

---

**7. Explain React.memo and its use cases**  
`React.memo` wraps functional components to prevent re-rendering unless props change.  
**Use-case:**  
Performance optimization for pure components.

---

**8. What is suspense?**  
A React feature for handling async operations, displaying fallback content while loading.
```js
<Suspense fallback={<div>Loading...</div>}>
  <LazyComp />
</Suspense>
```

---

**9. What is SSR (Server-Side Rendering) and CSR (Client-Side Rendering)? Why SSR?**  
- **SSR:** Renders components on the server, sends HTML to browser.
- **CSR:** Renders in browser.
**Why SSR:**  
Faster first load, better SEO, initial content for crawlers.

---

**10. Explain Middleware in React**  
Middleware is used in state management (Redux) for intercepting actions (e.g., async handling).

---

**11. What is Redux?**  
A predictable state container for JS apps, using actions, reducers, and store.

---

**12. Service Worker: What it is, its usage, and how to implement**  
A script that runs in the background, enabling offline support, push notifications, caching.
**Implementation:**  
Register with `navigator.serviceWorker.register('/sw.js')`.

---

**13. Rules for React Hooks**  
- Only call hooks at the top level.
- Only call hooks from React functions (components or custom hooks).

---

**14. Print screen preview responsive design, how will you handle it? (Use a library)**  
Use packages like `react-device-detect` or browser dev tools to test responsive layouts.

---

**15. If you have a form with three different fields, how do you manage and get the fields' values on form submission?**  
Use controlled components:
```js
const [form, setForm] = useState({a: '', b: '', c: ''});
<input value={form.a} onChange={e => setForm({...form, a: e.target.value})} />
// On submit: access form.a, form.b, form.c
```

---

**16. How to integrate an API, pass data from parent to child, and show the data in a Bootstrap table format?**  
- Fetch API data in parent.
- Pass data as prop to child.
- Render in table using Bootstrap classes.

---

**17. Create a React app with TypeScript, implement React Router, fetch an API, filter the data, and display selected fields.**  
- Create app with `create-react-app --template typescript`
- Use `react-router-dom` for routing.
- Fetch API with `fetch` or `axios`.
- Filter and display using `.filter()` and `.map()`.

---

**18. How to manage token and how to use that (JWT & AuthToken)?**  
- Store in httpOnly cookies for security, or localStorage/sessionStorage if needed.
- Use in Authorization headers for API calls.

---

**19. What startTransition method and how it works?**  
Allows marking updates as non-urgent for smoother UI.
```js
import { startTransition } from 'react';
startTransition(() => { setState(...) });
```

---

**20. What is Use method in react 19?**  
The `use` method allows using promises directly in components, especially for server components or data fetching.

---

**21. Which type of authentication and browser storage do you use (local storage vs cookies)?**  
- **Tokens:** Use http-only cookies for security.
- **Storage:** localStorage for non-sensitive data, cookies for authentication.
**Real-world:**  
JWT auth tokens often stored in cookies for secure APIs.

---

**22. Headless CMS: What is it and how is it used?**  
A headless CMS provides content via API, decoupled from the frontend presentation layer.
**Real-world:**  
Contentful, Strapi, Sanity—used with React frontends for dynamic content.

---
