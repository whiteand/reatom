# @reatom/core

Reatom's state manager core package.

[![npm](https://img.shields.io/npm/v/@reatom/core?style=flat-square)](https://www.npmjs.com/package/@reatom/core)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/@reatom/core?style=flat-square)](https://bundlephobia.com/result?p=@reatom/core)

## Install

```sh
npm i @reatom/core
```

or

```sh
yarn add @reatom/core
```

## Usage

[Open in CodeSandbox](https://codesandbox.io/s/reatomcore-demo-28t3d)

```js
import {
  declareAction,
  declareAtom,
  map,
  combine,
  createStore,
} from '@reatom/core'

/**
 * Step 1.
 * Declare actions
 */
const increment = declareAction()

/**
 * Step 2.
 * Declare atoms (like reducers or models)
 */
const counterAtom = declareAtom(0, (on) => [
  on(increment, (state) => state + 1),
])
const counterDoubledAtom = map(counterAtom, (value) => value * 2)
const countersShapeAtom = combine({
  counter: counterAtom,
  counterDoubled: counterDoubledAtom,
})

/**
 * Step 3.
 * Create store entry point
 */
const store = createStore(countersShapeAtom)

/**
 * Step 4.
 * Dispatch action
 */
store.dispatch(increment())

/**
 * Step 5.
 * Get action results
 */
console.log(store.getState(counterAtom))
// ➜ 1

console.log(store.getState(counterDoubledAtom))
// ➜ 2

console.log(store.getState(countersShapeAtom))
// ➜ { counter: 1, counterDoubled: 2 }
```

---

[Open source code on GitHub](https://github.com/artalar/reatom/tree/master/packages/core)
