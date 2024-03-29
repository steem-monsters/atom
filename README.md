<div>
  <p align="center">
    <img 
      src="https://document-export.canva.com/DADLRIBWTFM/45/preview/0001-645846858.png"
      height="350"
      width="350"
      alt="@steem-monsters/atom logo" />
  </p>
</div>

<h3 align="center">A way to manage shared, synchronous, independent state</h3>

<h3 align="center">Inspired by <a href="https://clojure.org/reference/atoms">atom</a>s in <a href="https://clojure.org/index">Clojure(Script)</a></h3>

<h3 align="center">Forked from <a href="https://github.com/libre-org/atom">@libre/atom</a></h3>

<div style="heigth:40px;">&nbsp;</div>

[![TypeScript](https://badges.frapsoft.com/typescript/version/typescript-next.svg?v=101)](https://github.com/ellerbrock/typescript-badges/)
[![npm (scoped)](https://img.shields.io/npm/v/@steem-monsters/atom.svg)](https://www.npmjs.com/package/@steem-monsters/atom)
[![npm bundle size (minified)](https://img.shields.io/bundlephobia/min/@steem-monsters/atom.svg)](https://bundlephobia.com/result?p=@steem-monsters/atom)
[![npm bundle size (minified + gzip)](https://img.shields.io/bundlephobia/minzip/@steem-monsters/atom.svg)](https://bundlephobia.com/result?p=@steem-monsters/atom)

[![npm](https://img.shields.io/npm/dt/@steem-monsters/atom.svg)](https://www.npmjs.com/package/@steem-monsters/atom)

[![NpmLicense](https://img.shields.io/npm/l/@steem-monsters/atom.svg)](https://www.npmjs.com/package/@steem-monsters/atom)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)

## Description

`@steem-monsters/atom` provides a data type called `Atom`s and a few functions for working with `Atom`s. It is heavily inspired by `atom`s in Clojure(Script). While the full power of Clojure `atom`s cannot be experienced in JavaScript's single-threaded runtime, `Atom`s do still offer similar benefits due to the highly asynchronous and event-driven nature of JavaScript.

Atoms provide a predictable way to manage state shared by multiple components of a
program as that state changes over time. They are particularly useful in the functional and reactive programming paradigms, where most components of a program are pure functions operating on immutable data. `Atoms` provide a controlled mechanism for mutability that lets multiple components access and update the same value without risking mutating another component's reference to it in the middle of some process or asynchronous operation.

### Put your state in an `Atom`:

```ts
import { Atom } from "@steem-monsters/atom";

const appState = Atom.of({
  color: "blue",
  userId: 1
});
```

### Read state with `deref`

You can't inspect `Atom` state directly, you have to `deref`erence it, like this:

```js
import { deref } from "@steem-monsters/atom";

const { color } = deref(appState);
```

### Update state with `swap`

You can't modify an `Atom` directly. The main way to update state is with `swap`. Here's its call signature:

```ts
function swap<S>(
  atom: Atom<S>, 
  updateFn: (state: DeepImmutable<S>) => S
): void;
```

`updateFn` is applied to `atom`'s state and the return value is set as `atom`'s new state. There are just two simple rules for `updateFn`:

1. it must return a value of the same type/interface as the previous state
2. it must not mutate the previous state

To illustrate, here is how we might update `appState`'s color:

```js
import { swap } from "@steem-monsters/atom";

const setColor = color =>
  swap(appState, state => ({
    ...state,
    color: color
  }));
```

> **Note:** Our `updateFn` is [spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)ing the old state onto a new object before overriding `color`. This is an easy way to obey the rules of `updateFn`. If manually spreading values seems tedious, there are many libraries that offer convenient functions for operating on JS data structures in an immutable manner, e.g. see [ramda](https://ramdajs.com/), [sanctuary](https://sanctuary.js.org/), [crocks](https://evilsoft.github.io/crocks/docs/), or (for the wizards among us) [fp-ts](https://gcanti.github.io/fp-ts/).

## Installation

**NPM**: `npm install --save @steem-monsters/atom`

**Yarn**: `yarn add @steem-monsters/atom`

**CDN**: `<script src="https://unpkg.com/@steem-monsters/atom" />`

- Exposed on the global object, like so: `window["@steem-monsters/atom"]`

## Usage

**ES6 `import`**

```js
import { Atom, deref, set, swap } from "@steem-monsters/atom";
```

**CommonJS `require`**

```js
const { Atom, deref, set, swap } = require("@steem-monsters/atom");
```

**Web `<script />` tag**

```js
const { Atom, deref, set, swap } = window["@steem-monsters/atom"];
```

## Documentation

[You can find API docs for `@steem-monsters/atom` here](https://steem-monsters.github.io/atom/)

## Contributing / Feedback

Please open an issue if you have any questions, suggestions for
improvements/features, or want to submit a PR for a bug-fix (please include
tests if applicable).
