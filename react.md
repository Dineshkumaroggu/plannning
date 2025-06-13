### ✅ **Level 1: React Fundamentals**

---

### 🟢 **Easy**

#### 1. What is React? Why would you use it?

**Answer:**
React is a JavaScript library for building user interfaces. It allows developers to build reusable UI components, manage state efficiently, and create dynamic web applications with a declarative approach.

**Why use it?**

* Reusable components
* Virtual DOM for better performance
* Unidirectional data flow
* Strong ecosystem (React Router, Redux, etc.)

---

#### 2. What is JSX?

**Answer:**
JSX stands for JavaScript XML. It is a syntax extension that lets you write HTML-like code in JavaScript. React uses JSX to describe UI structure.

**Example:**

```jsx
const element = <h1>Hello, World!</h1>;
```

JSX is syntactic sugar over `React.createElement`.

---

### 🟡 **Medium**

#### 3. How does the Virtual DOM work in React?

**Answer:**
The Virtual DOM is an in-memory representation of the real DOM. When the state of a component changes, React:

1. Creates a new Virtual DOM tree.
2. Compares it with the previous tree using a diffing algorithm.
3. Finds the minimal set of changes.
4. Updates the real DOM efficiently.

This improves performance by reducing direct DOM manipulations.

---

#### 4. What are controlled and uncontrolled components?

**Answer:**

* **Controlled Component:** Form elements whose value is controlled by React state.

```jsx
const [value, setValue] = useState('');
<input value={value} onChange={(e) => setValue(e.target.value)} />
```

* **Uncontrolled Component:** Form elements that maintain their own state, accessed via refs.

```jsx
const inputRef = useRef();
<input ref={inputRef} />
```

---

### 🔴 **Hard**

#### 5. Explain the reconciliation process in React.

**Answer:**
Reconciliation is the process by which React updates the DOM when state or props change.

Steps:

1. React builds a new virtual DOM.
2. React compares the new and old virtual DOMs using the **diffing algorithm**.
3. Minimal changes are computed and applied to the actual DOM.
4. React uses the `key` prop in lists to optimize performance and reduce re-rendering.

Misusing keys (e.g., using index) can lead to unnecessary renders or incorrect UI state.

---

## ✅ **Level 1 (Continued): Component Lifecycle, State, and Props**

We'll cover this in 3 parts: **Easy**, **Medium**, and **Hard**, including **code-based** and **theoretical** questions. This section is fundamental but crucial for real-world apps and interviews.

---

## 🟢 EASY

---

### 1. What is the difference between props and state?

**Answer:**

| Props                                       | State                                        |
| ------------------------------------------- | -------------------------------------------- |
| Passed from parent                          | Managed within component                     |
| Immutable                                   | Mutable                                      |
| Read-only                                   | Can be changed using `setState` / `useState` |
| Functional components receive via arguments | Stored via hook or class property            |

---

### 2. What are the main lifecycle methods in class components?

**Answer:**

* `constructor()`
* `componentDidMount()`
* `componentDidUpdate(prevProps, prevState)`
* `componentWillUnmount()`

---

### 3. What is the `useState` hook?

**Answer:**

`useState` is a React hook to manage local state in functional components.

```jsx
const [count, setCount] = useState(0);
```

---

### 4. Can you pass a function as a prop?

**Answer:**
Yes! This is how child components can call parent-defined behaviors.

```jsx
function Parent() {
  const sayHi = () => alert("Hi!");
  return <Child onClick={sayHi} />;
}
```

---

### 5. Code: Create a button that toggles text on click

```jsx
function ToggleText() {
  const [show, setShow] = useState(true);
  return (
    <div>
      <button onClick={() => setShow(!show)}>Toggle</button>
      {show && <p>Hello, World!</p>}
    </div>
  );
}
```

---

## 🟡 MEDIUM

---

### 6. What is `useEffect` and when is it called?

**Answer:**

`useEffect` is a hook used to handle side effects like data fetching, subscriptions, or DOM manipulation.

```jsx
useEffect(() => {
  console.log("Component mounted or updated");
}, []);
```

* Empty dependency `[]` → on mount
* Dependency `[value]` → when `value` changes
* Return function → cleanup on unmount

---

### 7. Difference between `useEffect` and `componentDidMount`?

**Answer:**

* `useEffect` runs **after every render** by default
* `componentDidMount` runs **once** after initial render
* You can mimic `componentDidMount` by passing `[]` in `useEffect`

---

### 8. Code: Fetch data on component mount using `useEffect`

```jsx
function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then(setUsers);
  }, []);

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

### 9. What is lifting state up in React?

**Answer:**

Lifting state means moving state from a child to the closest common parent to share it between components.

---

### 10. Code: Two sibling components sharing state

```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <CounterDisplay count={count} />
      <CounterButton increment={() => setCount(count + 1)} />
    </>
  );
}
```

---

## 🔴 HARD

---

### 11. What are the pitfalls of `useEffect` with dependencies?

**Answer:**

* Forgetting to include dependencies → stale closures
* Over-including dependencies → infinite loops
* Using objects/functions without `useCallback`/`useMemo`

---

### 12. Code: Prevent useEffect infinite loop due to object in dependency

```jsx
const obj = { name: "React" };

useEffect(() => {
  console.log("Triggered");
}, [JSON.stringify(obj)]); // workaround to prevent reference change
```

Better: use `useMemo` to preserve reference

---

### 13. Can you explain batching in React?

**Answer:**
React **batches multiple `setState` calls** into a single re-render to improve performance.

```jsx
setCount(count + 1);
setFlag(true);
// Both run in one render cycle
```

React 18 supports batching **across async code** too.

---

### 14. How do closures impact state updates in `useEffect` or `setInterval`?

**Answer:**

Closures may trap **stale state**:

```jsx
useEffect(() => {
  const id = setInterval(() => {
    console.log(count); // stale count!
  }, 1000);
  return () => clearInterval(id);
}, []);
```

**Fix using functional update:**

```jsx
setCount(prev => prev + 1);
```

---

### 15. Code: useEffect cleanup example

```jsx
useEffect(() => {
  const id = setInterval(() => console.log("tick"), 1000);
  return () => clearInterval(id); // cleanup
}, []);
```

---

## ✅ Summary: Concepts Covered

| Category                  | Concepts Covered                        |
| ------------------------- | --------------------------------------- |
| Props & State             | Basic difference, lifting state         |
| Lifecycle (Class + Hooks) | useEffect, mounting, cleanup            |
| State Sharing             | Parent-child, siblings                  |
| Coding Patterns           | useEffect fetch, button toggle, cleanup |
| Pitfalls                  | useEffect deps, closures, batching      |

---

## ✅ **Level 2: Component Architecture & Optimization**

We'll cover:

* HOC vs Custom Hooks
* Memoization techniques
* Performance optimization
* Component design patterns

### Format: **Theory + Real Code Snippets**

### Difficulty Levels: Easy → Medium → Hard

---

## 🟢 EASY

---

### 1. What is a Higher-Order Component (HOC)?

**Answer:**
An HOC is a function that takes a component and returns a new enhanced component.

```jsx
const withLogger = (Component) => {
  return function WrappedComponent(props) {
    console.log("Props:", props);
    return <Component {...props} />;
  };
};
```

Used for:

* Code reuse
* Logging
* Conditional rendering
* Access control (auth)

---

### 2. What is `React.memo()`?

**Answer:**
`React.memo` is a higher-order component that **memoizes** functional components. It prevents re-renders if props haven’t changed.

```jsx
const MyComponent = React.memo(function MyComponent({ name }) {
  console.log("Rendered!");
  return <p>{name}</p>;
});
```

---

### 3. When to use `useMemo`?

**Answer:**
Use `useMemo` to memoize **expensive computations** between renders:

```jsx
const result = useMemo(() => heavyComputation(data), [data]);
```

---

### 4. When to use `useCallback`?

**Answer:**
Use `useCallback` to memoize **functions** so they don’t trigger unnecessary renders.

```jsx
const handleClick = useCallback(() => doSomething(), [dependency]);
```

---

### 5. Code: Prevent re-renders with React.memo and useCallback

```jsx
const Child = React.memo(({ onClick }) => {
  console.log("Child Rendered");
  return <button onClick={onClick}>Click Me</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []);

  return <Child onClick={increment} />;
}
```

---

## 🟡 MEDIUM

---

### 6. What's the difference between HOC and Custom Hook?

**Answer:**

| Feature     | HOC                    | Custom Hook             |
| ----------- | ---------------------- | ----------------------- |
| Usage       | Wraps component        | Called inside component |
| Reusability | Code reuse via wrapper | Code reuse via logic    |
| Access      | Can modify JSX/Props   | Only logic              |

---

### 7. Build a custom hook for input handling

```jsx
function useInput(initial) {
  const [value, setValue] = useState(initial);
  const onChange = (e) => setValue(e.target.value);
  return { value, onChange };
}

function Form() {
  const name = useInput('');
  return <input {...name} placeholder="Name" />;
}
```

---

### 8. What is prop drilling and how to avoid it?

**Answer:**
Prop drilling is passing props through intermediate components just to reach deeply nested children.

✅ Solutions:

* Context API
* Redux or Zustand
* `useContext` + `createContext`

---

### 9. What is Context API? When to use it?

**Answer:**
It allows data (like theme, auth) to be passed across the component tree without prop drilling.

```jsx
const ThemeContext = createContext('light');
const value = useContext(ThemeContext);
```

---

### 10. Code: Theme toggler using Context

```jsx
const ThemeContext = React.createContext();

function ThemeProvider({ children }) {
  const [dark, setDark] = useState(false);
  return (
    <ThemeContext.Provider value={{ dark, toggle: () => setDark(!dark) }}>
      {children}
    </ThemeContext.Provider>
  );
}

function Button() {
  const { dark, toggle } = useContext(ThemeContext);
  return <button onClick={toggle}>{dark ? 'Dark' : 'Light'}</button>;
}
```

---

## 🔴 HARD

---

### 11. What is reconciliation performance bottleneck and how to avoid it?

**Answer:**
When component trees are large or props change frequently, React may re-render more than needed.

✅ Fix:

* Use stable keys
* Use `React.memo`
* Use `useMemo`, `useCallback`
* Avoid anonymous functions in JSX

---

### 12. How would you design a scalable component system (real-world pattern)?

**Answer:**

* Use **compound components** for flexibility
* Use **context** for shared state
* Follow **atomic design** (Atoms, Molecules, Organisms)
* Example: Modal, Tabs, Accordion

---

### 13. Code: Compound component pattern

```jsx
function Tabs({ children }) {
  const [active, setActive] = useState(0);
  return (
    <div>
      {children.map((child, i) =>
        React.cloneElement(child, { active: i === active, onClick: () => setActive(i) })
      )}
    </div>
  );
}

function Tab({ label, active, onClick }) {
  return <button style={{ fontWeight: active ? "bold" : "normal" }} onClick={onClick}>{label}</button>;
}
```

---

### 14. How do you lazy-load components?

```jsx
const LazyComponent = React.lazy(() => import('./MyComponent'));

<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

---

### 15. How do you measure React app performance?

**Answer:**

* Chrome DevTools
* `React DevTools` → Profiler tab
* `why-did-you-render` for re-renders
* Lighthouse

---

## ✅ Summary: Concepts Covered

| Category         | Topics                                     |
| ---------------- | ------------------------------------------ |
| Component Design | HOC, custom hooks, compound components     |
| Optimization     | memo, useMemo, useCallback, prop drilling  |
| Patterns         | Context API, lazy loading, scalability     |
| Code Examples    | Input hook, theme toggle, React.memo, Tabs |

---
Excellent! Let’s move on to:

---

## ✅ **Level 3: React Router, Forms, and State Management**

We'll explore:

* React Router (v6+)
* Form Handling (controlled, uncontrolled, validation)
* State Management (Redux, Context, Zustand)


---

## 🟢 EASY

---

### 1. What is React Router and why do we use it?

**Answer:**
React Router is a client-side routing library for React apps. It enables navigation without full page reloads and maps URLs to components.

---

### 2. Basic Route Setup (React Router v6+)

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./Home";
import About from "./About";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

### 3. What are controlled vs uncontrolled form components?

**Answer:**

* **Controlled**: React state drives input
* **Uncontrolled**: DOM handles input (via ref)

```jsx
// Controlled
<input value={value} onChange={e => setValue(e.target.value)} />

// Uncontrolled
<input ref={inputRef} />
```

---

### 4. Code: Create a login form with `useState`

```jsx
function LoginForm() {
  const [email, setEmail] = useState('');
  const [pass, setPass] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Email: ${email}, Pass: ${pass}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={email} onChange={e => setEmail(e.target.value)} placeholder="Email" />
      <input type="password" value={pass} onChange={e => setPass(e.target.value)} />
      <button type="submit">Login</button>
    </form>
  );
}
```

---

### 5. What is Redux and when should we use it?

**Answer:**
Redux is a predictable state container for JavaScript apps. Use it when:

* You have **global state** needs
* State needs to be **shared** across deeply nested components
* There’s **complex state logic** (e.g., undo/redo, time travel debugging)

---

## 🟡 MEDIUM

---

### 6. Explain `useReducer` and give an example

**Answer:**
`useReducer` is a hook alternative to `useState`, useful for **complex state logic**.

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "decrement": return { count: state.count - 1 };
    default: return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
    </>
  );
}
```

---

### 7. How does Redux work? (Flow diagram explanation)

**Answer:**

```
UI → dispatch(action) → reducer updates store → subscribers (UI) re-render
```

* **Action**: plain object (`{ type, payload }`)
* **Reducer**: pure function
* **Store**: holds state

---

### 8. Redux: Sample counter reducer with Redux Toolkit

```js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: 'counter',
  initialState: { count: 0 },
  reducers: {
    increment: (state) => { state.count += 1 },
    decrement: (state) => { state.count -= 1 },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

---

### 9. How to handle form validation in React?

**Answer:**
Options:

* Manual: check conditions and show errors
* Libraries: `Formik`, `react-hook-form`, `yup`

---

### 10. Code: Basic manual form validation

```jsx
const [email, setEmail] = useState('');
const [error, setError] = useState('');

const handleSubmit = () => {
  if (!email.includes("@")) {
    setError("Invalid email");
  } else {
    setError("");
    // submit logic
  }
};
```

---

## 🔴 HARD

---

### 11. What is Zustand and how is it different from Redux?

**Answer:**

| Feature     | Redux                         | Zustand             |
| ----------- | ----------------------------- | ------------------- |
| Boilerplate | High (especially w/o Toolkit) | Low (just a hook)   |
| Syntax      | Functional, verbose           | Hook-based, concise |
| Setup time  | Longer                        | Quick               |

```js
import create from 'zustand';

const useStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}));
```

---

### 12. Code: Zustand counter example

```jsx
const useStore = create((set) => ({
  count: 0,
  increase: () => set((s) => ({ count: s.count + 1 })),
}));

function Counter() {
  const { count, increase } = useStore();
  return <button onClick={increase}>Count: {count}</button>;
}
```

---

### 13. How does `react-hook-form` improve form performance?

**Answer:**

* Uses **refs** for uncontrolled components
* Minimizes re-renders
* Has built-in validation + integration with `yup`

```jsx
const { register, handleSubmit, formState: { errors } } = useForm();

<form onSubmit={handleSubmit(onSubmit)}>
  <input {...register("email", { required: true })} />
</form>
```

---

### 14. What is Code Splitting? How to implement it?

**Answer:**

Code splitting means dividing large bundles into smaller chunks to improve loading.

```js
const LazyComponent = React.lazy(() => import('./BigComponent'));

<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

---

### 15. How does React Router handle 404 routes?

```jsx
<Route path="*" element={<NotFound />} />
```

Place this as the last `<Route>` to catch all unknown routes.

---

## ✅ Summary

| Category         | Covered Items                        |
| ---------------- | ------------------------------------ |
| Routing          | Basic/404/Nesting                    |
| Forms            | Controlled, Validation, Libraries    |
| State Management | Redux, Zustand, useReducer           |
| Optimization     | react-hook-form, lazy load, suspense |
| Code Practices   | Forms, Counters, Custom Stores       |

---


