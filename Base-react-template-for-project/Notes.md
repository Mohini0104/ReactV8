- Create src folder: index.html, style.css, App.jsx
- `npm init -y`: will download package.json, where we will keep all our dependencies
- `prettier`: auto-formats your code

```Javascript
npm install -D prettier@2.7.1
```

- add file `.prettierrc`
- In the package.json file under script add

```Javascript
 "format": "prettier --write \"src/**/*.{js,jsx}\""
```

```Javascript
npm run format
```

- it will run that command. This means we don't have to remember that mess of a command and just have to remember format.

- `Eslint`: ESLint statically analyzes your code to quickly find problems. It is built into most text editors and you can run ESLint as part of your continuous integration pipeline.

- run

```Javascript
run npm install -D eslint@8.24.0 eslint-config-prettier@8.5.0
```

- Create file`.eslintrc.json` and add the following code

```Javascript
{
  "extends": ["eslint:recommended", "prettier"],
  "plugins": [],
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "node": true
  }
}
```

- add file `.gitignore` and inside the file add

```Javascript
node_modules
dist/
.env
.DS_Store
coverage/
.vscode/
```

- We are using `vite` this is the build tool we are using. It under the hood uses `Rollup`
  Installing `vite`

```Javascript
npm install -D vite@3.1.4 @vitejs/plugin-react@2.1.0
```

- In the index.html file in the script tag of APP.jsx add type="module" it'll help vite to understand we are not doing common JS here, we are working on ES6 module

- Add file `vite.config.js`
  write inside the file

```Javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  root: "src",
});
```

We now have a build process

- Installing React and React DOM
  It's a production dependency

```Javascript
npm install react@18.2.0 react-dom@18.2.0
```

- Add in package.json

```Javascript
 "dev": "vite", // start my dev server and get me going
 "build": "vite-build", // get me ready for production
 "preview": "vite-preview", // Help to see production build before going to production, runs vite build and then shows what vite build has built for you
```

- Run

```Javascript
npm run dev
```

- ESLint + React
  We need to give ESLint a hand to get it to recognize React and not yell about React not being used. Right now it thinks we're importing React and not using because it doesn't know what to do with React. Let's help it.

Run this:

```Javascript
npm install -D eslint-plugin-import@2.26.0 eslint-plugin-jsx-a11y@6.6.1 eslint-plugin-react@7.31.8
```
Replace the eslintrc with the below code:
```Javascript
{
    "extends": [
        "eslint:recommended",
        "plugin:import/errors",
        "plugin:react/recommended",
        "plugin:jsx-a11y/recommended",
        "prettier"
    ],
    "rules": {
        "react/prop-types": 0,
        "react/react-in-jsx-scope": 0
    },
    "plugins": [
        "react",
        "import",
        "jsx-a11y"
    ],
    "parserOptions": {
        "ecmaVersion": 2022,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true
        }
    },
    "env": {
        "es6": true,
        "browser": true,
        "node": true
    },
    "settings": {
        "react": {
            "version": "detect"
        },
        "import/resolver": {
            "node": {
                "extensions": [
                    ".js",
                    ".jsx"
                ]
            }
        }
    }
}
```
- To add github pages:
run 
```Javascript
npm install gh-pages --save-dev

```
add under script:
```Javascript
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build",
```
add homepage property:
```Javascript
https://{username}.github.io/{repo-name}
```
