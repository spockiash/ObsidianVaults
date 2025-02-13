The best way of creating React app with Deno is using Vite. It is possible to create React app without Vite in Deno but Vite allows for much smoother developer experience. It is also very fast.

When developing react applications with Deno (or Node) we use these frameworks as development servers. Vite is also development server technology. Once we build the application the output is JavaScript content for the browser. There is no React specific back-end component once the React front-end is pushed to production.
# Scaffolding with `create-vite-extra`
To scaffold project we can use `npm` package `create-vite-extra`. We can use [[Deno#CLI|Deno CLI]] with flags to scaffold new project with already prepared run flags:
```sh
deno run --allow-env --allow-read --allow-write npm:create-vite-extra
```
After this command Vite prompts to select scaffolding options, so we can choose what front-end framework we want and what language we want (JavaScript or TypeScript). Then we just `cd` into folder that matches name of the project and run the application with:
```sh
deno task dev
```

# Integrating Tailwind
To integrate Tailwind with Vite + Deno + React setup is tricky. The `deno` package manager is supporting `npm` but when using the native package management it is tricky to set things up right.

The best option so far I have found is to use `nvm` to manage `Node.js` and `npm` packages.

## Step by step guide
## Install packages
After we create the initial web app using `create-vite-extra` package. The we install the packages we will need:
```sh
npm install -D tailwindcss postcss autoprefixer @tailwindcss/vite @tailwindcss/postcss
```
The `-D` flag means that these are development dependencies.

## Create Tailwind Config Files
Next we need to create `tailwind.config.js` at our root folder:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```
Then we need to create `post.config.js`:
```js
import tailwindcss from "tailwindcss";
import autoprefixer from "autoprefixer";

export default {
  plugins: [tailwindcss, autoprefixer],
};
```
## Add Tailwind in Vite Config File
Navigate to the `vite.config.ts/js` file and add tailwinds:
```ts
import { defineConfig } from 'vite'
import deno from '@deno/vite-plugin'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

// https://vite.dev/config/
export default defineConfig({
	plugins: [deno(), react(), tailwindcss()],
	css: {
	postcss: "./postcss.config.js",
	},
})
```
## Create Styles File And Reference Them
Next create file `src/styles.css` and add the following:
```css
@import "tailwindcss";
```
Then we reference the file in our React entry point:
```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./styles.css"; // ✅ Import Tailwind CSS

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

When confronted with errors, be mindful and do not let them scare you. Maybe you need to reinstall some packages. When in doubt one can always try hard reset of the environment:
```sh
rm -rf node_modules package-lock.json deno.lock dist .vite
npm cache clean --force
deno cache --reload
npm install
deno task dev
```
This will force re installation of packages.