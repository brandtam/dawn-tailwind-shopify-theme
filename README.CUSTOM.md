# Dawn + Tailwind CSS

Add `node_modules` to `.gitignore`
```bash
echo "node_modules" >> .gitignore
```

Init a new pnpm project and install [Vite](https://vitejs.dev/) and [Tailwind CSS](https://tailwindcss.com/).
```bash
pnpm init && pnpm i -D vite tailwindcss postcss autoprefixer
```

Add config files and shopifyignore
```bash
touch vite.config.js postcss.config.js tailwind.config.js tailwind.css .shopifyignore
```
---
Add the following to `tailwind.css`
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
---
Add the following to `tailwind.config.js`
```js
/** @type {import('tailwindcss').Config} */
export default {
	content: [
		"./**/*.{js,json,liquid}", // updated to include theme files 
	],
	theme: {
		extend: {},
	},
	plugins: [],
}
```
---
Add the following to `postcss.config.js`
```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```
---
Add the following to `vite.config.js`
```js
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    outDir: 'assets',
    emptyOutDir: false,
    minify: false,
    rollupOptions: {
      input: 'tailwind.css',
      output: {
        dir: 'assets',
        assetFileNames: 'styles.css',
      },
    },
  },
});
```
---
Add scripts to `package.json`.

Make sure to replace `yourstore.myshopify.com` with your store's url
```json
"scripts": {
	"dev": "shopify theme dev -s yourstore.myshopify.com",
	"build": "vite build --minify",
	"watch": "vite build --watch"
}
```
---
Add the following to `.shopifyignore`.

In this example the lock file is pnpm's `pnpm-lock.yaml` but you can use `yarn.lock` or `package-lock.json` as well depending on the package manager you use.
```bash
package.json
pnpm-lock.yaml
```


