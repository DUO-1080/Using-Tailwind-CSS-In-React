# Setting Up Tailwind CSS In A React Project

### 1. create react project

```
touch .env

// .env
SKIP_PREFLIGHT_CHECK=true
```



### 2. install tailwind and tools

```bash
npm install tailwindcss postcss-cli autoprefixer -D
```

### 3. setup tailwind source file ( src/styles/tailwind.css )

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

### 4. create tailwind config file

```bash
npx tailwind init
```

### 5. process tailwind css

```bash
touch postcss.config.js
```

in `post.config.js`

```js
const tailwindcss = require("tailwindcss");
module.exports = {
  plugins: [tailwindcss("./tailwind.config.js"), require("autoprefixer")],
};
```

### 6. edit script

`package.json`

```
  "scripts": {
    "start": "npm run watch:css && react-scripts start",
    "build": "npm run build:css && react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "build:css": "postcss src/styles/tailwind.css -o src/styles/main.css",
    "watch:css": "postcss src/styles/tailwind.css -o src/styles/main.css"
  },
```

### 7. purge unused css classes

`tailwind.js`

```js
module.exports = {
  purge: ["src/**/*.js", "src/**/*.jsx", "src/**/*.ts", "src/**/*.tsx", "public/**/*.html"],
  theme: {
    extend: {},
  },
  variants: {},
  plugins: [],
};
```

> Now whenever you compile your CSS with `NODE_ENV` set to `production`, Tailwind will automatically purge unused styles from your CSS.np

