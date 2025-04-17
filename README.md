# React Style Guidelines

## 1. Overview
A concise, up‑to‑date guide for building scalable, maintainable React apps using modern best practices.

## 2. Project Structure
Organize by feature/domain, not by file type.
```bash
src/
├─ assets/           # images, fonts, icons
├─ config/           # env variables, app settings
├─ components/       # reusable UI components (atomic)
│  ├─ Button/
│  │  ├─ Button.tsx
│  │  ├─ Button.module.css
│  │  ├─ Button.test.tsx
│  │  └─ index.ts
│  └─ …
├─ hooks/            # custom hooks (useXxx)
├─ pages/            # route components
├─ services/         # API clients, domain logic
├─ store/            # global state (Redux, Zustand, etc.)
├─ styles/           # design tokens, global styles
├─ types/            # shared TypeScript types
└─ utils/            # pure helper functions
```  

- Use absolute imports via `tsconfig.json` or `jsconfig.json`.
- Index files only for major folders, avoid deep barrel exports.

## 3. Naming Conventions
| Item           | Convention         |
|----------------|--------------------|
| Files          | `PascalCase.tsx`   |
| Components     | `PascalCase`       |
| Hooks          | `usePascalCase`    |
| Variables/funcs| `camelCase`        |
| Interfaces     | `PascalCase` (I-prefix optional) |
| Enums          | `PascalCase`       |

## 4. Components
- **Functional components** with React Hooks only (no classes).
- **Named exports** for all components; use default export only if one per file.
- **Props typing**: use `interface` or `type` for props, and destructure in signature.

```tsx
interface ButtonProps {
  onClick: () => void;
  label: string;
}

export const Button: React.FC<ButtonProps> = ({ onClick, label }) => (
  <button onClick={onClick}>{label}</button>
);
```

## 5. Hooks
- Prefix with `use`, single responsibility.
- Keep logic in custom hooks, not in components.
- Follow [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html).

## 6. State & Data Fetching
- Prefer **React Query** or **SWR** for server state.
- Use **Context API** sparingly for global cross-cutting data.
- Keep component state minimal; lift state up only when needed.

## 7. Styling
- Choose one: **CSS Modules**, **Styled‑Components**, or **Tailwind CSS**.
- Store design tokens (colors, spacing) in `styles/`.
- Avoid inline styles; prefer classNames or styled APIs.

## 8. Testing
- **Jest** + **React Testing Library**.
- Co‑locate tests: `Component.test.tsx` next to component.
- Cover:
  - Rendering
  - User interactions
  - Edge cases
  - Accessibility (aria, roles)

## 9. Linting & Formatting
- **ESLint** with `eslint-config-airbnb` or community preset.
- **Prettier** for consistent formatting.
- Enforce:
  - Hook dependencies
  - No unused vars
  - Import order (e.g. `simple-import-sort`)

## 10. TypeScript
- Enable strict mode.
- Avoid `any`; use `unknown` or precise types.
- Export types from `types/` folder when shared.

## 11. Performance & Best Practices
- **Memoize** heavy computations (`useMemo`, `useCallback`).
- **Code‑split** routes with `React.lazy` & `Suspense`.
- **Accessibility**: semantic HTML, labels, alt text.
- **Error boundaries** for unexpected crashes.

## 12. CI/CD & Deployment
- Run lint, type‑check, and tests in CI pipeline.
- Build artifacts with versioned output.
- Use env‑specific configs for staging/production.

---
*Last updated: April 2025*
