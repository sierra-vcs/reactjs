# Chapter 01 - Introduction (Quick Revision)

Welcome to **Chapter 01** of the React Training Program.  
This chapter provides a **quick revision of fundamental React concepts** that will be used throughout the course.

---

## Introduction to React

- **React** is a **JavaScript library** for building **user interfaces**.
- It is **component-based** and allows building reusable UI elements.
- React uses a **virtual DOM** for efficient rendering.

### Example: Basic Component

```javascript
import React from 'react';

function Hello() {
    return <h1>Hello, React!</h1>;
}

export default Hello;
```

---

## JSX (JavaScript XML)

- JSX allows writing HTML-like syntax in JavaScript.
- React automatically converts JSX to `React.createElement` calls.

**Example:**

```javascript
const element = <h2>Welcome to React</h2>;
```

- JSX must have one parent element.
- Use `{}` to insert JavaScript expressions.

---

## Components in React

### Functional Components

- Written as functions.
- Can use Hooks to manage state and lifecycle.

**Example:**

```javascript
function Greeting({ name }) {
    return <p>Hello, {name}!</p>;
}
```

### Class Components

- Written as ES6 classes.
- Can use state and lifecycle methods.

**Example:**

```javascript
import React, { Component } from 'react';

class Welcome extends Component {
    render() {
        return <h2>Welcome, {this.props.name}</h2>;
    }
}

export default Welcome;
```

---

## Props

- Props are inputs to components.
- They are read-only.

**Example:**

```javascript
<Greeting name="React Learner" />
```

---

## State

- State is local to a component and can change over time.
- Only available in class components or functional components with `useState`.

**Example:**

```javascript
import React, { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
}

export default Counter;
```

---

## Events in React

- React uses synthetic events instead of native events.
- Event names are in camelCase (`onClick`, `onChange`).
- You pass a function reference as the handler.

**Example:**

```javascript
function ButtonClick() {
    const handleClick = () => alert('Button clicked!');
    return <button onClick={handleClick}>Click Me</button>;
}
```

---

## Conditional Rendering

- Render elements based on conditions.

**Example:**

```javascript
function Login({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in</p>}
        </div>
    );
}
```

---

## Lists and Keys

- Render arrays using `map()`.
- Use a unique key for each element.

**Example:**

```javascript
const items = ['Apple', 'Banana', 'Cherry'];

function ItemList() {
    return (
        <ul>
            {items.map((item, index) => <li key={index}>{item}</li>)}
        </ul>
    );
}
```

---

## Hooks in React (Detailed)

React Hooks allow functional components to use state and other features.

### 1. useState

- Manages local state.
- Returns `[state, setState]`.

**Example:**

```javascript
const [count, setCount] = useState(0);
```

### 2. useEffect

- Handles side-effects like API calls or subscriptions.
- Runs after render.
- Can run once, on mount, or on state change.

**Example:**

```javascript
useEffect(() => {
    console.log('Component mounted or count changed');
}, [count]); // Dependency array
```

### 3. useRef

- Access DOM elements or persist values across renders.

**Example (DOM reference):**

```javascript
const inputRef = useRef();
<input ref={inputRef} />
```

**Example (value persistence):**

```javascript
const renderCount = useRef(0);
renderCount.current += 1;
```

### 4. useContext

- Access global state provided by a Context.
- Avoids prop drilling.

**Example:**

```javascript
const ThemeContext = React.createContext('light');

function App() {
    return (
        <ThemeContext.Provider value="dark">
            <Toolbar />
        </ThemeContext.Provider>
    );
}

function Toolbar() {
    const theme = useContext(ThemeContext);
    return <p>Current theme: {theme}</p>;
}
```

### 5. useReducer

- Manage complex state logic.
- Similar to Redux reducer pattern.

**Example:**

```javascript
const initialState = { count: 0 };

function reducer(state, action) {
    switch(action.type) {
        case 'increment': return { count: state.count + 1 };
        case 'decrement': return { count: state.count - 1 };
        default: return state;
    }
}

const [state, dispatch] = useReducer(reducer, initialState);

// Usage:
<button onClick={() => dispatch({ type: 'increment' })}>+</button>
```

### 6. Other Hooks

- `useMemo` → Memoize expensive calculations.
- `useCallback` → Memoize functions to prevent unnecessary re-renders.
- `useLayoutEffect` → Like `useEffect` but runs synchronously after DOM updates.
- `useDebugValue` → Display debug info for custom hooks.

---

## React Router (v6+)

- Used for client-side routing.
- Key components: `BrowserRouter`, `Routes`, `Route`, `Link`, `NavLink`.

**Example:**

```javascript
<Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
</Routes>
```

---

## Higher-Order Components (HOC)

- A function that wraps a component to add extra functionality.

**Example:**

```javascript
function withAuth(Component) {
    return function Wrapper(props) {
        const isLoggedIn = true;
        return isLoggedIn ? <Component {...props} /> : <p>Please log in</p>;
    };
}
```

---

## Forms in React

- Use controlled components for form inputs.
- The value is stored in state.

**Example:**

```javascript
function NameForm() {
    const [name, setName] = useState('');

    const handleSubmit = e => {
        e.preventDefault();
        alert(`Submitted: ${name}`);
    };

    return (
        <form onSubmit={handleSubmit}>
            <input value={name} onChange={e => setName(e.target.value)} />
            <button type="submit">Submit</button>
        </form>
    );
}
```

---

## Summary

- React is component-based and uses JSX.
- Props pass data, state stores local values.
- Events, forms, and conditional rendering are essential.
- Hooks enable state, lifecycle, and more in functional components.
- Routing and HOCs add navigation and reusable logic.

This chapter covers all basic concepts needed before diving deeper.