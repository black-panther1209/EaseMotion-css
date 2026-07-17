# SCSS @use 'easemotion-css/scss' Path Failures in Vite & Next.js

A beginner-friendly guide to fixing common SCSS load-path resolution issues when using EaseMotion CSS with modern frameworks like Vite and Next.js.

## Why This Error Happens

Many developers encounter errors such as:

```scss
@use 'easemotion-css/scss';
```

Common error messages:

```text
Can't find stylesheet to import.
Failed to resolve 'easemotion-css/scss'
SassError: Can't find stylesheet to import.
```

These problems usually happen because:

* `easemotion-css` is not installed
* The package manager did not correctly resolve `node_modules`
* The SCSS entry path is incorrect
* The project configuration overrides default Sass resolution behavior
* Cache files are stale after dependency updates

---

## Step 1: Install EaseMotion CSS

```bash
npm install easemotion-css sass
```

Or:

```bash
yarn add easemotion-css sass
```

Or:

```bash
pnpm add easemotion-css sass
```

---

## Step 2: Use the Correct SCSS Import

```scss
@use 'easemotion-css/scss';
```

Create an SCSS file (for example `src/styles/main.scss`) and add the import above.

---

## Vite Setup

### vite.config.js

```js
import { defineConfig } from 'vite';

export default defineConfig({
  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `@use 'easemotion-css/scss' as *;`
      }
    }
  }
});
```

### main.js

```js
import './styles/main.scss';
```

---

## Next.js Setup

### app/layout.tsx or pages/_app.tsx

```tsx
import '@/styles/main.scss';
```

### styles/main.scss

```scss
@use 'easemotion-css/scss' as *;
```

---

## Common Failure Cases

| Error                                     | Cause                        | Fix                                                                 |
| ----------------------------------------- | ---------------------------- | ------------------------------------------------------------------- |
| `Can't find stylesheet to import`         | Package not installed        | Run `npm install easemotion-css sass`                               |
| `Failed to resolve 'easemotion-css/scss'` | Incorrect import path        | Use `@use 'easemotion-css/scss' as *;`                              |
| Styles not applied                        | SCSS file not imported       | Import the SCSS file in the app entry file                          |
| Works locally but fails in CI             | Lockfile/dependency mismatch | Delete `node_modules`, reinstall dependencies, and commit lockfiles |
| Vite build fails after package update     | Cached dependencies          | Remove `.vite` cache and reinstall dependencies                     |

---

## Troubleshooting Checklist

* Ensure `easemotion-css` and `sass` are installed
* Use the correct import:

```scss
@use 'easemotion-css/scss' as *;
```

* Verify your SCSS file is imported into the application
* Restart the development server after installation
* Delete and reinstall dependencies if resolution errors persist:

```bash
rm -rf node_modules package-lock.json
npm install
```

For Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```

---

## Validation Checklist

* [x] EaseMotion CSS installed
* [x] Sass installed
* [x] Correct `@use` syntax
* [x] SCSS file imported into the app entry point
* [x] Development server restarted
* [x] Vite and Next.js examples verified

---

## Folder Structure

```text
submissions/
└── scss/
    └── ease-scss-load-paths-sp/
        └── README.md
```

This guide provides copy-paste-ready solutions for resolving EaseMotion SCSS path issues in Vite and Next.js projects.
