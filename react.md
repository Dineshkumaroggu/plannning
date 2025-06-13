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

