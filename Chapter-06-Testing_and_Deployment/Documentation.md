# Chapter 06 - Testing & Deployment

This chapter focuses on ensuring **React applications are reliable, maintainable, and production-ready**.  
We will explore **Testing (unit, integration, end-to-end)** and **Deployment best practices**.

---

## 🔹 Testing in React

### Why Testing?
- Ensures **code correctness**
- Prevents bugs when refactoring
- Builds confidence before deployment
- Saves time in the long run

### Types of Testing
1. **Unit Testing**: Tests small pieces of code (functions, components)
2. **Integration Testing**: Tests interactions between components
3. **End-to-End (E2E) Testing**: Simulates real user flows in the browser

---

### ✅ Tools for Testing React

#### Jest
- JavaScript testing framework by Facebook
- Runs tests fast, supports mocks, snapshots, and code coverage

**Example (Jest unit test):**
```javascript
// sum.js
export function sum(a, b) {
    return a + b;
}

// sum.test.js
import { sum } from './sum';

test('adds 2 + 3 to equal 5', () => {
    expect(sum(2, 3)).toBe(5);
});
```

#### React Testing Library (RTL)
- Focuses on testing components as users would interact with them
- Encourages testing behavior over implementation details

**Example (RTL test for a button):**
```javascript
import { render, screen, fireEvent } from "@testing-library/react";
import Counter from "./Counter";

test("increments counter when button is clicked", () => {
    render(<Counter />);
    fireEvent.click(screen.getByText("Increment"));
    expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

#### Vitest
- A faster alternative to Jest, especially for Vite projects
- Compatible with Jest APIs

#### Cypress / Playwright (E2E Testing)
- Automates browsers to test real user flows
- Great for login flows, form submissions, navigation

**Example (Cypress test):**
```javascript
describe("Login Flow", () => {
    it("logs in a user", () => {
        cy.visit("/login");
        cy.get("input[name=email]").type("test@example.com");
        cy.get("input[name=password]").type("password123");
        cy.get("button[type=submit]").click();
        cy.contains("Welcome back!");
    });
});
```

---

## 🔹 Deployment Best Practices

### Preparing for Deployment

#### Build the project
```bash
npm run build
```
Creates an optimized production bundle in `/build`.

#### Environment Variables
Use `.env` for sensitive keys (API URLs, tokens).

**Example:**
```bash
REACT_APP_API_URL=https://api.example.com
```

#### Code Splitting
Use `React.lazy` and `Suspense` for lazy loading.  
Improves performance by loading only what’s needed.

### Deployment Platforms
- **Netlify / Vercel**: One-click deploys, CI/CD, free tiers
- **GitHub Pages**: Simple static hosting for React apps
- **AWS Amplify / S3 + CloudFront**: Scalable cloud hosting
- **Firebase Hosting**: Easy integration with Firebase backend

**Example: Deploy React App to Netlify**
1. Push project to GitHub
2. Go to Netlify
3. Connect your GitHub repo
4. Build command: `npm run build`
5. Publish directory: `build/`

### Best Practices for Production
- Use **HTTPS**: Secure your app
- Set up **CI/CD**: Automate testing + deployment pipeline
- Monitor performance (Lighthouse, Google Analytics)
- Use **Error boundaries**: Catch and display UI-friendly errors
- Optimize images & assets: Reduce load times

---

## 🔹 Summary

- **Testing**: Use Jest + RTL for unit/integration tests, Cypress/Playwright for E2E
- **Deployment**: Optimize builds, use environment variables, deploy on modern platforms
- **Best Practices**: Secure, monitor, and continuously deploy your React apps

A well-tested and properly deployed React app is reliable, fast, and production-ready.
