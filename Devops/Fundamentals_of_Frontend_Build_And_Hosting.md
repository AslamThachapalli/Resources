# What happens when you run npm run build in a React app?

### 1. What a bundler or build tool (Vite/Webpack/Rollup) actually does?
- A **Bundler**
  - Converts JSX → plain JavaScript (via Babel/esbuild).
  - Combines many files → one bundle (bundle.js).
  - Removes unused files or codes (tree-shaking).
  - Compresses the code so they take less memory (minification). \
👉 So, when you run vite build, it produces the final (dist/) folder that browsers can read directly.

### 2. Difference between Vite, Webpack, Rollup
- **Webpack**: The old workhorse. Very configurable, but complex. Does everything (CSS, images, code splitting).
- **Rollup**: More focused on building libraries (like your component library). Creates smaller, optimized bundles.
- **Vite**: Modern dev tool. Uses esbuild under the hood for super fast builds. Also gives a built-in dev server (hot reload).

### 3. What is actually inside the dist/ folder?
- When you run `npm run build`, you usually get:
  - `index.html` → entry HTML file.
  - `assets/` folder:
    - `bundle.[hash].js` → your entire React app code.
    - `style.[hash].css` → compiled CSS.
    - Optimized images/fonts. 
      
👉 That’s all you need to host your site — nothing “React-specific” anymore. Just plain HTML, JS, CSS.

### 4. What is a Web Server, and why do we need one?
- If you open `index.html` by double-clicking, it works locally.
- But to share with the world, you need a server — basically a delivery person who hands out your `index.html`, `bundle.js`, `style.css` to anyone asking.

Types:
- Static server: Just gives files (e.g., Vercel, Firebase Hosting, Azure Static Web Apps).
- Dynamic server: Runs logic before responding (e.g., Node/Express APIs). \
👉 For frontend apps, 99% of the time you just need static hosting + CDN.

#### Basics of web serving
- If it is a React app, or Vanilla website with `style.css`, `main.js`, and `index.html`, double clicking on `index.html` doesn't run the website.
- For React app, double clicking on index.html in `dist/` folder will show a blank screen.
- This is because, `index.html` refers to other files via `<link/>`, and browser doesn't resolve `file://` path by default.
- That's where the webserver comes into picture. Where links will be converted to `http://host.com/[filepath]`. Now the browser do a network request to this url, and server responds with the file.

To simulate production hosting in localhost:
- Install serve globally → `npm install -g serve`.
- Run `serve dist/`.
- Visit `http://localhost:3000`.
This simulates production hosting.
