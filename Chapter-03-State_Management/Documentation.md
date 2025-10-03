# Chapter 03 - State Management

Welcome to **Chapter 03** of the React Training Program.  
In this chapter, you'll learn how to manage **application state** effectively.

React provides local state management (`useState`, `useReducer`), but as your app grows, sharing state across components can be challenging. That's where **state management libraries** like **Redux, Zustand, Recoil, and Formik** are useful.

---

## 🔹 What is State Management?

State management is about **how data flows** in your app and how components **access, modify, and share** that data.

- **Local State**: Managed inside a component using hooks.
- **Global State**: Shared across multiple components (e.g., authentication, user settings).

Without proper state management, apps can become:  
❌ Hard to debug  
❌ Full of prop drilling  
❌ Inconsistent

---

## 1. Redux

Redux is a popular state management library for React.  
It enforces **predictable state changes** using three principles:

1. **Single Source of Truth**: State is stored in a single store.
2. **State is Read-Only**: State can only be changed by dispatching actions.
3. **Changes with Pure Functions**: Reducers handle how state updates.

### Example: Counter with Redux Toolkit

**store.js**
```javascript
import { configureStore, createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
    name: 'counter',
    initialState: { value: 0 },
    reducers: {
        increment: (state) => { state.value += 1; },
        decrement: (state) => { state.value -= 1; },
    }
});

export const { increment, decrement } = counterSlice.actions;
export const store = configureStore({
    reducer: { counter: counterSlice.reducer }
});
```

**App.js**
```javascript
import React from 'react';
import { Provider, useDispatch, useSelector } from 'react-redux';
import { store, increment, decrement } from './store';

function Counter() {
    const count = useSelector((state) => state.counter.value);
    const dispatch = useDispatch();

    return (
        <div>
            <h2>Count: {count}</h2>
            <button onClick={() => dispatch(increment())}>+</button>
            <button onClick={() => dispatch(decrement())}>-</button>
        </div>
    );
}

export default function App() {
    return (
        <Provider store={store}>
            <Counter />
        </Provider>
    );
}
```
👉 Redux Toolkit is the recommended way to use Redux today (less boilerplate).

---

## 2. Zustand

Zustand is a lightweight alternative to Redux.

- Simple API with minimal setup.
- Uses hooks for state management.

### Example
```javascript
import create from 'zustand';

const useStore = create((set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    decrement: () => set((state) => ({ count: state.count - 1 })),
}));

function Counter() {
    const { count, increment, decrement } = useStore();

    return (
        <div>
            <h2>Count: {count}</h2>
            <button onClick={increment}>+</button>
            <button onClick={decrement}>-</button>
        </div>
    );
}

export default Counter;
```
👉 Great for small to medium projects.

---

## 3. Recoil

Recoil is a state management library from Facebook.

- Treats state as atoms (shared pieces of state).
- Easy to scale and works well with async state.

### Example
```javascript
import { atom, useRecoilState } from 'recoil';

const counterAtom = atom({
    key: 'counterAtom',
    default: 0,
});

function Counter() {
    const [count, setCount] = useRecoilState(counterAtom);

    return (
        <div>
            <h2>Count: {count}</h2>
            <button onClick={() => setCount(count + 1)}>+</button>
            <button onClick={() => setCount(count - 1)}>-</button>
        </div>
    );
}
```
👉 Best for projects where state is dynamic and async-heavy.

---

## 4. Formik (Form State Management)

Formik is used specifically for managing form state and validation.  
It reduces boilerplate when handling forms in React.

### Example
```javascript
import React from 'react';
import { useFormik } from 'formik';

function SignupForm() {
    const formik = useFormik({
        initialValues: { email: '' },
        validate: (values) => {
            const errors = {};
            if (!values.email) errors.email = 'Required';
            return errors;
        },
        onSubmit: (values) => {
            alert(JSON.stringify(values, null, 2));
        },
    });

    return (
        <form onSubmit={formik.handleSubmit}>
            <input
                type="email"
                name="email"
                onChange={formik.handleChange}
                value={formik.values.email}
            />
            {formik.errors.email ? <div>{formik.errors.email}</div> : null}
            <button type="submit">Submit</button>
        </form>
    );
}

export default SignupForm;
```
👉 Ideal for forms with validation, submission, and error handling.

---

## ✅ Summary

- **Redux**: Best for large apps, predictable state.
- **Zustand**: Lightweight, easy to use, great for small/medium projects.
- **Recoil**: Great for complex and async-heavy state.
- **Formik**: Specifically for handling forms.