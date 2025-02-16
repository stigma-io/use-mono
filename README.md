# use-mono

[![npm version](https://img.shields.io/npm/v/use-mono?style=flat-square)](https://www.npmjs.com/package/use-mono) [![build status](https://img.shields.io/github/actions/workflow/status/stigma-io/use-mono/tests.yml?branch=master&style=flat-square)](https://github.com/stigma-io/use-mono/actions?workflow=Tests) [![npm bundle size](https://img.shields.io/bundlephobia/minzip/use-mono?style=flat-square)](https://bundlephobia.com/result?p=use-mono) [![code coverage](https://img.shields.io/coveralls/github/stigma-io/use-mono?style=flat-square)](https://coveralls.io/github/stigma-io/use-mono) [![typescript supported](https://img.shields.io/npm/types/typescript?style=flat-square)](https://github.com/stigma-io/use-mono) [![100k+ downloaded](https://img.shields.io/npm/dt/use-mono?style=flat-square)](https://www.npmjs.com/package/use-mono)

When you want to separate your React hooks between several components it's can be very difficult, because all context data stored in React component function area.
If you want to share some of state parts or control functions to another component your need pass It thought React component props. But If you want to share It with sibling one level components or a set of scattered components, you will be frustrated.

`useBetween` hook is the solution to your problem :kissing_closed_eyes:

```javascript
import React, { useState, useCallback } from 'react';
import { useBetween } from 'use-mono';

const useCounter = () => {
  const [count, setCount] = useState(0);
  const inc = useCallback(() => setCount(c => c + 1), []);
  const dec = useCallback(() => setCount(c => c - 1), []);
  return {
    count,
    inc,
    dec
  };
};

const useSharedCounter = () => useBetween(useCounter);

const Count = () => {
  const { count } = useSharedCounter();
  return <p>{count}</p>;
};

const Buttons = () => {
  const { inc, dec } = useSharedCounter();
  return (
    <>
      <button onClick={inc}>+</button>
      <button onClick={dec}>-</button>
    </>
  );
};

const App = () => (
  <>
    <Count />
    <Buttons />
    <Count />
    <Buttons />
  </>
);

export default App;
```
[![Edit Counter with useBetween](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/counter-with-usebetween-zh4tp?file=/src/App.js)

`useBetween` is a way to call any hook. But so that the state will not be stored in the React component. For the same hook, the result of the call will be the same. So we can call one hook in different components and work together on one state. When updating the shared state, each component using it will be updated too.

If you like this idea and would like to use it, please put star in github. It will be your first contribution!

### Developers :sparkling_heart: use-mono

> Hey [@stigma-io](https://github.com/stigma-io), just wanted to say thank you for this awesome library! ✋
> Switching from React Context + useReducer to this library reduced soooo much boilerplate code.
> It's much more nice, clean and simple now, plus the bonus of using "useEffect" incapsulated within the state hook is just awesome.
>
> I don't get why this library doesn't have more stars and more popularity. People using useContext+useReducer are really missing out 😃
>
> [**Jesper**, _This library should have way more stars! 🥇_](https://github.com/stigma-io/use-mono/issues/14)


> [@stigma-io](https://github.com/stigma-io) as I mentioned before this lib is awesome and it allowed me to simplify an app that was using Redux. I was able to replace everything we were doing with Redux with just use-mono and its tiny 2K footprint!
>
> Plus personally I think the code is cleaner because with use-mono it just looks like normal hooks and not anything special like Redux code. I personally find it easier to read and understand than Redux!
> 
> [**Melloware**, _Release discussion_](https://github.com/stigma-io/use-mono/discussions/20#discussioncomment-1715792)

> I was about to install Redux until I found this library and it is a live saver. Really awesome job [@stigma-io](https://github.com/stigma-io). I don't know if I ever need to use Redux again haha
> 
> [**Ronald Castillo**](https://github.com/stigma-io/use-mono/issues/14#issuecomment-1050601343)

### Supported hooks

```diff
+ useState
+ useEffect
+ useReducer
+ useCallback
+ useMemo
+ useRef
+ useImperativeHandle
```

If you found some bug or want to propose improvement please [make an Issue](https://github.com/stigma-io/use-mono/issues/new) or join to [release discussion on Github](https://github.com/stigma-io/use-mono/discussions/35). I would be happy for your help to make It better! :wink:

+ [How to use SSR](./docs/ssr.md)
+ [Try Todos demo on CodeSandbox](https://codesandbox.io/s/todos-use-bettwen-8d2th?file=/src/components/todo-list.jsx)
+ [The article “Reuse React hooks in state sharing” on dev.to](https://dev.to/stigma-io/reuse-react-hooks-in-state-sharing-1ell)

### Install

```bash
npm install use-mono
# or
yarn add use-mono
```

Enjoy and happy coding!
