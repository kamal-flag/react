1- install tailwindCss and postCSS

```
npm i -D tailwindcss@3.1.8 postcss@8.4.18 autoprefixer@10.4.12
```

2- initialize a tailwindCss file config (postcss.config.js and tailwind.config.js)

```
npx tailwindcss init -p
```

add this line to tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,ts,jsx,tsx,html}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

3- add this lines to style.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

4- add Tailwind CSS IntelliSense extension to VS code

5- add prettier for tailwindCSS (we suppose you already have prettier installed in your app)

```
npm install -D prettier-plugin-tailwindcss
```

and then add this code into 'prettier.config.js'

```javascript
module.exports = {
  plugins: [require("prettier-plugin-tailwindcss")],
};
```

6- we use a special tailwind plugin to handle styles for froms

install it

```
npm install -D @tailwindcss/forms@0.5.3
```

and add this plugin to tailwind.config.js.

// replace plugins
plugins: [require("@tailwindcss/forms")],

7- we can create our css classes using tailwindCss

we use base to reconfigure basic html element like => body, div, h1, ...etc.
we use component layer to create our css classes for components like input for example.
we use utilities layer to create css classes for utilities such active, disabled, ...etc

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  body {
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  }
}

@layer components {
  .search-input {
    @apply mb-5 block w-60;
  }
}

@layer utilities {
  .grayed-out-disabled {
    @apply disabled:opacity-50;
  }
}
```
