# ⚛️ React Commands & Setup Guide

This document provides essential React CLI commands, project setup tips, and common workflows to help you efficiently develop React applications. It covers environment setup, npm scripts, linting, debugging, testing, and deployment tips.

---

## 🛠 Environment Setup

| Command                       | Description                                                          |
| ----------------------------- | -------------------------------------------------------------------- |
| `npx create-react-app my-app` | Create a new React project using Create React App (CRA).             |
| `npm start`                   | Start the React development server (usually runs at localhost:3000). |
| `npm run build`               | Build the React app for production (optimized and minified).         |
| `npm test`                    | Run tests using Jest (default testing framework in CRA).             |
| `npm run eject`               | Eject from CRA to customize the build configuration (irreversible).  |
| `npm install -g serve`        | Install a static server globally for serving the production build.   |

---

## ⚙️ Common React CLI Commands

| Command                   | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- |
| `npm install <package>`   | Install a new npm package and add it to `package.json`.                   |
| `npm uninstall <package>` | Remove a package from the project.                                        |
| `npm update`              | Update all packages to their latest versions respecting semver.           |
| `npm audit`               | Run security audit on installed dependencies.                             |
| `npm run lint`            | Run linter (if configured, e.g., ESLint).                                 |
| `npx eslint .`            | Run ESLint directly on the current directory (requires ESLint installed). |
| `npx react-devtools`      | Launch React Developer Tools standalone app for debugging.                |
| `npm outdated`            | Check for outdated npm packages in your project.                          |

---

## 🔨 Useful npm Scripts

| Script               | Description                                                    |
| -------------------- | -------------------------------------------------------------- |
| `start`              | Start development server with hot reloading.                   |
| `build`              | Create optimized production build.                             |
| `test`               | Run tests in watch mode.                                       |
| `eject`              | Expose CRA config for customization.                           |
| `lint`               | Run linting on source files (custom script, optional).         |
| `prettier --write .` | Format codebase with Prettier (requires Prettier installed).   |
| `npm run format`     | Run custom format script (usually configured to run Prettier). |

---

## 🧪 Testing & Debugging

| Command / Tool             | Description                                                                          |
| -------------------------- | ------------------------------------------------------------------------------------ |
| `npm test`                 | Run Jest tests in watch mode by default.                                             |
| `npm test -- --coverage`   | Generate a test coverage report.                                                     |
| `npm run test:ci`          | Run tests once for CI environments (custom script).                                  |
| React Developer Tools      | Browser extension or standalone app for inspecting React components and hooks state. |
| `console.log()` & Debugger | Basic JS debugging via console and browser devtools.                                 |

---

## 📋 Typical React Workflow

1. **Create a new React app:**

   ```bash
   npx create-react-app my-app
   cd my-app
   ```

2. **Start development server:**

   ```bash
   npm start
   ```

3. **Add dependencies as needed:**

   ```bash
   npm install axios react-router-dom
   ```

4. **Run tests:**

   ```bash
   npm test
   ```

5. **Build for production:**

   ```bash
   npm run build
   ```

6. **Serve production build locally (optional):**

   ```bash
   serve -s build
   ```

7. **(Optional) Eject to customize configs:**

   ```bash
   npm run eject
   ```

---

## 💡 Tips & Tricks

* Use `npx` to run CLI tools without global installs (e.g., `npx eslint`).
* Use React Developer Tools browser extension or standalone (`npx react-devtools`) for component tree inspection.
* Regularly update dependencies using `npm update` and check security with `npm audit`.
* Use ESLint and Prettier together for consistent code style and automated formatting.
* When deploying, serve the contents of the `build` folder with a static web server (e.g., `serve`, Nginx).
* Use environment variables with `.env` files to manage different configs (`REACT_APP_` prefix required).
* Use React’s Profiler API and devtools for performance monitoring.
* Consider adding custom scripts to `package.json` to automate repetitive tasks.

---

## 🔗 Useful Resources

* [React Official Docs](https://reactjs.org/docs/getting-started.html)
* [Create React App](https://create-react-app.dev/docs/getting-started)
* [React Developer Tools](https://reactjs.org/blog/2019/08/15/new-react-devtools.html)
* [ESLint](https://eslint.org/)
* [Prettier](https://prettier.io/)
* [Jest](https://jestjs.io/docs/getting-started)
* [Serve - Static Server](https://www.npmjs.com/package/serve)

---
