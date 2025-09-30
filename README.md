
![Logo](https://res.cloudinary.com/duhmeadz6/image/upload/v1759164576/icon_rtc_potrzz.jpg)



**Plug-and-Play, ready-to-use, highly customizable theme component for [React.js](https://react.dev/)**

# React Theme Component

A React theme toggler with dark/light mode support based on TailwindCSS.


## Table of contents

- [Installation](#installation)
- [Features](#features)
- [Examples and Usage](#examples-and-usage)
- [Contact Me](#contact-me)
- [License](#license)

[![npm][npm-image]][npm-url]

[npm-image]: https://res.cloudinary.com/duhmeadz6/image/upload/v1759219823/npm_version_badge_gj4zpj.svg
[npm-url]: https://www.npmjs.com/package/react-theme-component

## Installation

This is a [React.js](https://react.dev/) component available through the
[npm registry](https://www.npmjs.com/).

Before installing, [create a React.js](https://react.dev/learn/react-compiler/installation) project and this component has default features to automate theme switching for [TailwindCSS](https://tailwindcss.com/docs/installation/using-vite), so make sure to configure it as per your requirements.
Any version of react, react-dom and tailwindcss is compatible.

Installation is done using the
[`npm install` command](https://docs.npmjs.com/getting-started/installing-npm-packages-locally):

```bash
npm install react-theme-component
```

## Features

  * Ready to use, just need to inject in your code
  * Focus on high customizability
  * Compatible with any version of React.js and TailwindCSS
  * Provide custom fields for getter and setter for loose coupling
  * Would work fine with normal state, ContextAPI and State Management Libraries like Redux, Zustand
  * Provides best UI and UX by providing ways to change color accordingly.
  * Ready to push for production


## Default Inputs and Fields

```jsx
export default function ThemeToggler({
    mode = "class",
    getter,
    setter,
    localKey = "theme",
    icons = true,
    lightOuterColor = "#d1d5dc",
    lightInnerColor = "black",
    darkOuterColor = "black",
    darkInnerColor = "#d1d5dc",
    extras = ""
}) {
    .....
}
```

## Examples and Usage

Here is a quick start snippet

```jsx
import React from "react";
import ThemeToggler from "react-theme-component";

export default function App() {
  return (
    <>
        <p>Change Theme: </p>
        <ThemeToggler />
    </>
  );
}
```

**can be injected with user's self-defined state:**

```jsx
import React, { useState } from "react";
import ThemeToggler from "./ThemeToggler";
export default function App() {
    const [isDark, setIsDark] = useState(false);
    return (
        <>
            <h1 className="text-4xl w-fit mx-auto px-5 py-3 my-2 text-slate-800 dark:text-neutral-400 dark:shadow-slate-900 rounded-2xl">{isDark ? "Dark Theme" : "Light Theme"}</h1>

            <ThemeToggler getter={isDark} setter={setIsDark} localKey={"theme-key"} />
        </>);
}
```
**can use react-redux in case global management is required:**

"themeSlice.js"

```jsx

import { createSlice } from "@reduxjs/toolkit";

export const themeSlice = createSlice({
    name: "theme",
    initialState: {
        isDark: false
    },
    reducers: {
        changeTheme: (state, action) => {
            state.isDark = action.payload;
        }
    }
});

export const {changeTheme} = themeSlice.actions;
```

"store.js"

```jsx
import { configureStore } from "@reduxjs/toolkit";
import { themeSlice } from "./themeSlice";

const store = configureStore({
    reducer: {
        theme: themeSlice.reducer
    }
});

export default store;
```

using in "App.js":

```jsx
import React, { useState } from "react";
import ImageTitle from "./components/ImageTitle";
import ThemeToggler from "./ThemeToggler";
import { useDispatch, useSelector } from "react-redux";
import { changeTheme } from "./store/themeSlice";
export default function App() {
    const isDark = useSelector(state => state.theme.isDark);
    const dispatch = useDispatch();

    function setIsDark(input) {
        dispatch(changeTheme(input));
    }

    return (
        <>
            <h1 className="text-4xl w-fit mx-auto px-5 py-3 my-2 text-slate-800 dark:text-neutral-400 dark:shadow-slate-900 rounded-2xl">{isDark ? "Dark Theme" : "Light Theme"}</h1>

            <ImageTitle />

            <ThemeToggler mode="attribute" getter={isDark} setter={setIsDark} icons={true} darkOuterColor={"#3579e6"} darkInnerColor={"#203352"} />
        </>);
}
```

## Contact Me

Feel free to reach out to me through the following channels:
- **Email:** bkvats2394@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/bhupender-kumar-sharma-2a144a2a7
- **X:** https://x.com/BSharma10111

Let me know if you need help refining this further! 😊

## License

  [MIT](LICENSE)
