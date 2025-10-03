# Chapter 05 - Advanced Topics

This chapter explores **advanced topics in React** that improve user experience, app performance, and inclusivity.  
We will cover **Localization (i18n), Progressive Web Apps (PWA), Server-Side Rendering (SSR), and Accessibility best practices (ARIA roles & semantics).**

---

## 🔹 Localization (i18n)

### What is Localization?
Localization (i18n → internationalization) allows an application to **adapt text, formats, and UI** to different languages and regions.

### Why i18n in React?
- Reach global users.
- Automatically adapt to **date, time, currency, and language preferences**.
- Provide **multi-language support** for accessibility.

### Popular Libraries
- **react-i18next** – Widely used with React.
- **FormatJS / react-intl** – Rich formatting for dates, numbers, plurals.

#### Example: Using `react-i18next`
```javascript
import { useTranslation } from "react-i18next";

function Welcome() {
    const { t } = useTranslation();
    return <h1>{t("welcome_message")}</h1>;
}
```
**Translation file (`en.json`):**
```json
{
    "welcome_message": "Welcome to React Training!"
}
```

---

## 🔹 Progressive Web Apps (PWA)

### What is a PWA?
A web application that behaves like a native app:
- Works offline.
- Installable on home screen.
- Uses service workers for caching & background sync.

### Why PWA in React?
- Faster page loads (cached assets).
- Works on low network or no internet.
- Native-like experience on mobile.

### Adding PWA in React
- CRA (Create React App) has a service worker option.
- Use libraries like Workbox for caching strategies.

#### Example: Enabling Service Worker in CRA
```javascript
// index.js
import * as serviceWorkerRegistration from './serviceWorkerRegistration';
serviceWorkerRegistration.register();
```

---

## 🔹 Server-Side Rendering (SSR)

### What is SSR?
Instead of sending an empty HTML shell + JS bundle, SSR sends fully rendered HTML from the server.  
This improves SEO, first paint speed, and performance on slow devices.

### SSR in React
**ReactDOMServer:**  
React provides APIs like `renderToString()` to render components on the server.
```javascript
import ReactDOMServer from "react-dom/server";
import App from "./App";

const html = ReactDOMServer.renderToString(<App />);
```
Used with Node.js & Express to serve pre-rendered HTML.

**React Server Components:**  
A newer model where some components run only on the server, reducing client bundle size.

---

## 🔹 Next.js (Quick Intro)

While SSR can be implemented manually, Next.js is the most popular React framework for SSR.

- **File-based routing:** Pages are created via folder structure.
- **Static Site Generation (SSG):** Build-time HTML generation.
- **Hybrid rendering:** SSR + CSR (client-side).

#### Example: Next.js Page
```javascript
export default function Home({ posts }) {
    return <h1>Welcome to Next.js</h1>;
}

export async function getServerSideProps() {
    return { props: { posts: [] } };
}
```
*(We will not go deep into Next.js here, just understand it is the go-to tool for SSR in React.)*

---

## 🔹 Accessibility (A11y)

### Why Accessibility?
Accessibility ensures apps are usable by everyone, including people with disabilities.  
This is achieved via:
- Semantic HTML.
- ARIA roles & attributes.
- Keyboard navigation support.

### Semantic HTML
Use proper HTML elements instead of generic `<div>` or `<span>`.

**✅ Correct**
```html
<button>Submit</button>
<nav>Navigation Bar</nav>
<header>Page Header</header>
```
**❌ Incorrect**
```html
<div onClick="submit()">Submit</div>
```

### ARIA Roles
ARIA (Accessible Rich Internet Applications) adds metadata for assistive technologies.

**Examples:**
```html
<div role="button" tabindex="0">Click Me</div>
<div role="alert">Form submitted successfully!</div>
```

### Best Practices
- Use labels for inputs.
- Ensure color contrast meets WCAG standards.
- Provide focus indicators for keyboard users.

---

## 🔹 Summary

- **Localization (i18n):** Multi-language support with libraries like react-i18next.
- **PWAs:** Make apps installable, offline-capable, and fast.
- **SSR:** Improve SEO & performance; ReactDOMServer or frameworks like Next.js.
- **Accessibility:** Use semantic HTML, ARIA roles, and ensure inclusivity.
