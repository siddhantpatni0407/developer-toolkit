# React Project — Naming Conventions, Folder Structure & Standards

> Opinionated, practical guide for consistent React projects. Adapt as needed for your team.

---

## Table of Contents

1. Purpose
2. File & Component Naming Conventions
3. Folder Structure (recommended)
4. Component Types & Examples
5. Assets (images, fonts, icons)
6. Styling & Class Naming
7. Exports, Barrel Files & Indexing
8. State Management & Data Flow
9. Tests and Test Structure
10. Tooling: Linting, Formatting, Types, CI
11. Accessibility & Performance
12. Commit Messages, Branching & PR Guidelines
13. Documentation Standards
14. Security & Environment Variables
15. Example ESLint / Prettier / Husky rules (quick)
16. Onboarding checklist

---

## 1. Purpose

This README is a single-source guide for naming, organization, and coding standards in React projects. It aims to make codebases predictable, easy to navigate, and maintainable across teams.

---

## 2. File & Component Naming Conventions

- **General:**

  - Component files: `PascalCase` → `UserCard.tsx`
  - Utility files: `kebab-case` → `date-utils.ts`
  - Hooks: `camelCase` starting with `use` → `useAuth.ts`

- **Tests:** `MyComponent.test.tsx` (or `.spec.tsx`)
- **Types:** `*.types.ts` or `types.ts` inside feature/component
- **Assets:** `kebab-case` → `hero-banner.png`, `icon-user.svg`
- **Configs:** lowercase → `webpack.config.js`, `jest.config.js`

**Tip:** Align filename with exported symbol for readability.

---

## 3. Folder Structure (recommended)

```
src/
├─ assets/
│  ├─ images/
│  ├─ icons/
│  └─ fonts/
├─ components/
│  ├─ Button/
│  │  ├─ Button.tsx
│  │  ├─ Button.module.css
│  │  ├─ Button.test.tsx
│  │  └─ index.ts
├─ features/
│  ├─ auth/
│  │  ├─ components/
│  │  ├─ hooks/
│  │  ├─ services/
│  │  └─ authSlice.ts
├─ pages/
│  ├─ HomePage/
│  │  ├─ HomePage.tsx
│  │  └─ HomePage.module.css
├─ hooks/
├─ services/
├─ store/
├─ utils/
├─ types/
├─ routes/
├─ constants/
├─ styles/
├─ i18n/
├─ tests/
├─ App.tsx
├─ index.tsx
└─ setupTests.ts
```

**Scalability Notes:**

- Use **feature-driven** structure for large apps (auth, dashboard, profile, etc.).
- Keep **shared UI** in `/components`.
- Keep **global helpers** in `/utils`, **business logic** in `/features`.

---

## 4. Component Types & Examples

- **UI Components:** Pure, reusable (`Button`, `Modal`).
- **Containers:** Connect to store / API (`UserListContainer`).
- **Pages:** Route-level entry (`DashboardPage`).
- **Layout Components:** Shared shells (`MainLayout`, `AuthLayout`).

**Best Practice:** One component = one folder with `index.ts` for cleaner imports.

---

## 5. Assets (images, fonts, icons)

- Use `src/assets` for global assets.
- Place **component-scoped assets** in that component’s folder.
- Optimize SVGs with `svgo`.
- Use `alt` text for accessibility, or `alt=""` with `aria-hidden` for decorative.
- Prefer `webp/avif` for modern image formats.

---

## 6. Styling & Class Naming

- **Preferred Strategies:**

  - CSS Modules (`Component.module.css`)
  - Tailwind CSS (utility-first)
  - Styled Components / Emotion (CSS-in-JS)

- **Class naming:**

  - CSS Modules → `styles.card`
  - Global CSS → BEM (`header__logo--small`)

- **Theme:** Define global colors, spacing, fonts in `:root` or theme config.
- **Avoid inline styles** (except for dynamic calculations).

---

## 7. Exports, Barrel Files & Indexing

- Use `index.ts` inside component folders.
- Avoid root-level catch-all barrel files.
- Configure `tsconfig.paths` for import aliases (`@components`, `@features`).

---

## 8. State Management & Data Flow

- **Small apps:** Local state (`useState`, `useReducer`).
- **Server state:** React Query / SWR.
- **Global state:** Redux Toolkit / Zustand / Recoil.
- **Principle:** Keep state closest to where it’s used. Don’t over-engineer.
- **API Layer:**

  - Keep in `/services`
  - Use Axios/Fetch wrapper with interceptors
  - Always type API responses

---

## 9. Tests and Test Structure

- **Unit tests:** colocated `.test.tsx`
- **Integration tests:** under `/tests` or feature-specific `__tests__`
- **E2E tests:** `cypress/` or `playwright/`
- **Coverage targets:** 80%+ for critical logic
- **Golden rules:**

  - Test **user behavior**, not implementation
  - Use `@testing-library/react` for React components

---

## 10. Tooling: Linting, Formatting, Types, CI

- **TypeScript:** enable `strict`
- **Linting:** ESLint with React + TS + a11y plugins
- **Formatting:** Prettier + consistent editor config
- **Pre-commit:** Husky + lint-staged
- **CI/CD:**

  - Run `lint`, `typecheck`, `test`
  - Build with `--production`
  - Run Lighthouse CI for performance budgets

---

## 11. Accessibility & Performance

- Use semantic HTML tags (header, nav, section, main)
- Ensure keyboard navigation & focus states
- Test with Lighthouse/Axe
- Code-split routes/components
- Use React `memo` and `useCallback` carefully to avoid unnecessary re-renders
- Prefer lazy-loading heavy dependencies

---

## 12. Commit Messages, Branching & PR Guidelines

- **Commit style:** Conventional Commits

  - `feat(auth): add refresh token`
  - `fix(user): prevent null crash`
  - `chore(ci): update GitHub Actions`

- **Branching:**

  - `feature/short-desc`
  - `bugfix/ISSUE-ID`
  - `hotfix/urgent-fix`

- **PRs:**

  - Clear title & description
  - Screenshots for UI changes
  - Tests included

---

## 13. Documentation Standards

- Maintain `README.md` in root and feature-level subfolders.
- Use JSDoc/TSDoc for complex functions/hooks.
- Document prop types with `Storybook` or `Docgen`.
- Update docs as part of PR review process.

---

## 14. Security & Environment Variables

- Keep secrets in `.env.local`, not committed.
- Use `process.env.REACT_APP_*` for environment variables.
- Never commit API keys/tokens.
- Review dependencies regularly (`npm audit`, `snyk`).
- Use HTTPS for all API calls.

---

## 15. Example ESLint / Prettier / Husky rules (quick)

- **ESLint (partial)**

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:jsx-a11y/recommended",
    "prettier"
  ]
}
```

- **lint-staged**

```json
{
  "lint-staged": {
    "src/**/*.{ts,tsx,js,jsx}": ["eslint --fix", "prettier --write"],
    "src/**/*.{css,scss}": ["prettier --write"]
  }
}
```

---

## 16. Onboarding checklist

1. Install Node (LTS or project-specified)
2. Clone repo, install deps (`npm i` / `yarn`)
3. Copy `.env.example` → `.env.local`
4. Run `npm run dev` / `yarn dev`
5. Run tests with `npm test`
6. Run linting with `npm run lint`
7. Review coding standards in this README

---

## Appendix: Quick Examples & Patterns

### Functional Component

```tsx
import React from "react";

export type BadgeProps = { label: string };
export default function Badge({ label }: BadgeProps) {
  return <span className="badge">{label}</span>;
}
```

### Custom Hook

```ts
import { useState, useCallback } from "react";

export function useCounter(initial = 0) {
  const [count, setCount] = useState(initial);
  const inc = useCallback(() => setCount((c) => c + 1), []);
  const dec = useCallback(() => setCount((c) => c - 1), []);
  return { count, inc, dec };
}
```

### Code Splitting

```tsx
import { lazy, Suspense } from "react";
const Dashboard = lazy(() => import("./pages/Dashboard/Dashboard"));

<Suspense fallback={<div>Loading...</div>}>
  <Dashboard />
</Suspense>;
```

---

## Need to adapt? — Tips

- Tailwind? Document common utility patterns.
- Monorepo? Each package has its own `README` + shared root tooling.
- Legacy app? Roll out linting + paths first, then refactor gradually.

---
