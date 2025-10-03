# Chapter 02 - Code Quality

Welcome to **Chapter 02** of the React Training Program.  
In this chapter, we focus on **maintaining clean, consistent, and professional code** using best practices and tools.

Good code quality makes projects:
- Easier to read and maintain
- Less prone to bugs
- More scalable for teams
- Professional and industry-ready

---

## 📂 Folder Organization

A well-structured React project improves maintainability and collaboration.

### Recommended Project Structure
```plaintext
src/
├── assets/      # Images, fonts, icons
├── components/  # Reusable UI components
├── pages/       # Page-level components (routes)
├── hooks/       # Custom hooks
├── context/     # Context API state
├── store/       # Redux/Zustand/Recoil state
├── utils/       # Helper functions
├── services/    # API calls, external integrations
├── styles/      # Global CSS / SCSS
├── App.js
└── index.js
```

👉 **Tip:** Keep files small and components focused on a single responsibility.

---

## 🧹 ESLint

**ESLint** identifies and fixes problems in JavaScript/React code.  
It enforces **coding standards** and helps avoid **bad practices**.

### Install ESLint
```bash
npm install eslint --save-dev
npx eslint --init
```
During setup, choose:
- To check syntax and find problems
- Framework → React
- Language → JavaScript (or TypeScript if using TS)
- Format → JSON/YAML/JS config file

**Example `.eslintrc.json`:**
```json
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "extends": [
        "eslint:recommended",
        "plugin:react/recommended"
    ],
    "parserOptions": {
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "plugins": ["react"],
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "single"]
    }
}
```

**Run ESLint:**
```bash
npx eslint src/
```

---

## 🎨 Prettier

**Prettier** is a code formatter.  
It ensures consistent formatting (indentation, quotes, trailing commas, etc.).

### Install Prettier
```bash
npm install prettier --save-dev
```

**Example `.prettierrc`:**
```json
{
    "singleQuote": true,
    "semi": true,
    "trailingComma": "es5",
    "printWidth": 80,
    "tabWidth": 2
}
```

**Run Prettier:**
```bash
npx prettier --write .
```

---

## ⚡ ESLint + Prettier Integration

Sometimes ESLint and Prettier rules conflict. To fix this:

```bash
npm install eslint-config-prettier eslint-plugin-prettier --save-dev
```

Update `.eslintrc.json`:
```json
{
    "extends": [
        "eslint:recommended",
        "plugin:react/recommended",
        "plugin:prettier/recommended"
    ]
}
```
Now ESLint will also check formatting rules from Prettier.

---

## 🛠 VSCode Setup

For the best developer experience:
- Install ESLint extension
- Install Prettier extension
- Enable Format on Save in VSCode settings

**Example `settings.json`:**
```json
{
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```

---

## ✅ Summary

- Folder organization keeps code clean and scalable.
- ESLint enforces coding standards and avoids bugs.
- Prettier ensures consistent formatting across teams.
- Integration of ESLint + Prettier + VSCode leads to professional code quality.