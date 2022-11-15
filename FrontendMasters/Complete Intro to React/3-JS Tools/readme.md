# NPM

- npm init -y ( to create a new npm project)
- npm install --save-dev prettier@2.7.1 (we use --save-dev to add this package only in the developer mode, once in production it will be removed, we can also do "-D" instead)
- if we use ^ in the package.json for a library then we do "npm i" again it will install the latest version for that package and ignore the version, if we want to install the exact package we should remove ^.

# Prettier

- in order to configure prettier in our project, we add a file named .prettierrc in our project and we put our configuration inside, if we put empty object like {}, it will use the default config
- install also the prettier extension
- and do this in your settings (settings.json)

1. ctrl + shift + p
2. type json and select : Preferences: Open setting
3. add this lines :

   - "javascript.format.enable": false, // disable javascript format code, and we will enable prettier format
   - "prettier.singleQuote": true,
   - "editor.formatOnSave": true, // enable prettier format, since it's all ready installed

- we can also add a script in our project that format the entire project with a command

to do it we add the following in our package.json

```javascript
"scripts": {
"format": "prettier --write \"src/\*_/_.{js,jsx}\"",
//.....
},
```

and we call it in the terminal :

```
npm run format
```

# ESLint

- to install ESLint :

```
 npm install -D eslint@8.24.0 eslint-config-prettier@8.5.0
```

add a file in our root project named ".eslintrc.json", and we add on it

```json
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

and also install an extension Named "ESLint" from the microsoft

and to run the eslint with npm in our hole project we add a script in our package.json

```javascript
"scripts": {
"format": "prettier --write \"src/\*_/_.{js,jsx}\"",
"lint": "eslint \"src/**/*.{js,jsx}\" --quiet",
//.....
},
```

and to run it

```
npm run lint
```

# Git

create a file named .gitignore to put the folders and files which we don't want to put in the repository

```
node_modules/
dist/
.env
.DS_Store
coverage/
.vscode/
```

# Vite

to install it

```
npm install -D vite@3.1.4 @vitejs/plugin-react@2.1.0
```

1.  in our index.html, in the script tag we add type="module"

```
 <script type="module" src="./App.js"></script>
```

We need to add module to the script tag so that the browser knows it's working with modern browser technology that allows you in development mode to use modules directly. Instead of having to reload the whole bundle every time, your browser can just reload the JS that has changed. It allows the browser to crawl the dependency graph itself which means Vite can run lightning fast in dev mode. It will still package it up for production so we can support a range of browsers.

2. we add a config file for vite named "config.vite.js"

3. and now we need to install react into our project

```
npm install react@18.2.0 react-dom@18.2.0
```

4. we will add a few others scripts in our project in the package.json

```javascript
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    //...
//.....
},
```
