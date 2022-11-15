# JSX

- jsx is like wrting HTML in javascript

- ESLint is not configured by default to understund React, we need to add some aditional packages in order to do that

```
npm install -D eslint-plugin-import@2.26.0 eslint-plugin-jsx-a11y@6.6.1 eslint-plugin-react@7.31.8
```

- we cannot use the word "class" to define css classes, because it's a reserved word in javascript instead we use className, some for the keyword "for" in labels, we use "htmlFor"

-

# Hooks

- we need another ESLint plugin for react hooks

```
npm install -D eslint-plugin-react-hooks@4.6.0
```

and add this plugin to the configuration of ESLint

```json
{
  "extends": [
    // …
    "plugin:react-hooks/recommended"
    //…
  ]
}
```

- Let's think about how React works: when you type in the input, React detects that a DOM event happens. When that happens, React thinks something may have changed so it runs a re-render. Providing your render functions are fast, this is a very quick operation. It then diffs what's currently there and what its render pass came up with. It then updates the minimum amount of DOM necessary.

# Effects

- we use effects to do somethings outiside the components like fetch APIs

# React dev tools

- React Strinct mode : React has a new strict mode. If you wrap your app in <React.StrictMode></React.StrictMode> it will give you additional warnings about things you shouldn't be doing.

- Actually in react 18 if we activate Strict mode, the use effect are called twice, that anoying
