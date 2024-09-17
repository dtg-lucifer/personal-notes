---
tags:
  - reactjs
  - frontend
  - ssr
  - express
  - interview
---
# Basic SSR example with React and Express


## Project Structure

```
react-ssr-example/
├── build
├── dist
├── node_modules
├── public
│ └── index.html 
├── server/ 
│ └── server.ts 
├── src/ 
│ ├── styles/ 
│ │ ├── __globals.css 
│ │ └── app.css 
│ ├── App.tsx 
│ └── index.tsx 
├── .gitignore 
├── esbuild.config.mjs 
├── package-lock.json 
├── package.json 
├── pnpm-lock.yaml 
├── README.md 
└── tsconfig.json
```

**File:** template.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="bundle.css">
  <title>React SSR Template</title>
</head>
<body>
  <div id="root"></div>
  <script src="/bundle.js"></script>
</body>
</html>
```

**File:** App.tsx

```tsx
import React from "react";
import "./styles/app.css";

const App = () => {
  const [state, setState] = React.useState(0);
  return (
    <main>
      <h1>Clicked {state} times</h1>
      <button className="text-3xl" onClick={() => setState(prev => ++prev)}>
        Add
      </button>
    </main>
  );
};

export default App;
```

**File:** index.tsx

```tsx
import React from 'react';
import { hydrateRoot } from 'react-dom/client';
import App from './App';
import "./styles/__globals.css";

hydrateRoot(document.getElementById('root')!, <App />);
```

**File:** server.ts

```ts
import path from "path";
import fs from "fs";

import { createElement } from "react";
import { renderToString } from "react-dom/server";

import express from "express";
import App from "../src/App";

const PORT = process.env.PORT ?? 8000;
const app = express();

app.use(express.static("dist"));

app.use("/", (req, res, next) => {
  fs.readFile(path.resolve("./public/index.html"), "utf-8", (err, data) => {
    if (err) {
      console.log(err);
      return res.status(500).send("Some error happened");
    }
    return res.send(
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${renderToString(createElement(App))}</div>`
      )
    );
  });
});

app.listen(PORT, () => {
  console.log(`App launched on ${PORT}`);
});
```


**File:** esbuild.config.mjs

```js
import esbuild from "esbuild";
import cssModulesPlugin from "esbuild-css-modules-plugin";

esbuild
  .build({
    entryPoints: ["./src/index.jsx"],
    bundle: true,
    outfile: "dist/bundle.js",
    minify: true,
    loader: { ".js": "jsx", ".png": "file", ".svg": "file", ".jpg": "file" },
    plugins: [
      cssModulesPlugin(),
    ],
  })
  .catch(() => process.exit(1));
  
esbuild
  .build({
    entryPoints: ["./server/server.js"],
    minify: true,
    bundle: true,
    outfile: "build/server.js",
    platform: "node",
    target: "node14",
    format: "cjs",
    external: ["react", "react-dom/server", `express`, "fs", "path"],
    plugins: [],
  })
  .catch(() => process.exit(1));
```

**Needed scripts for the project to run**

```json
"scripts": {
	"build": "node esbuild.config.mjs",
	"start": "nodemon --watch src -e jsx,tsx,css,ts,js --exec \"npm run build && node build/server.js\"",
	"watch:build": "nodemon --watch src -e jsx,tsx,js,ts,css esbuild.config.mjs"
},
```

### _For more info, [visit](https://github.com/dtg-lucifer/ssr-react-template)_