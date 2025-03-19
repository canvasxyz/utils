# @canvas-js/utils

[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg)](https://github.com/RichardLitt/standard-readme) [![license](https://img.shields.io/github/license/canvasxyz/utils)](https://opensource.org/licenses/MIT) [![NPM version](https://img.shields.io/npm/v/@canvas-js/utils)](https://www.npmjs.com/package/@canvas-js/utils) ![TypeScript types](https://img.shields.io/npm/types/@canvas-js/utils)

This repo is for utility methods and types related to JavaScript programming in general.

Anything that is only used by a single package should go in that package's src/utils.ts file; and anything that is related to a specific feature or domain should go in its own utility package.

## Table of contents

- [API](#api)
  - [`assert`](#assert)
  - [`signalInvalidType`](#signalinvalidtype)
  - [`mapEntries`](#mapentries)
  - [`mapKeys`](#mapkeys)
  - [`mapValues`](#mapvalues)
  - [`zip`](#zip)
  - [`replaceUndefined`](#replaceendefined)
  - [`stripUndefined`](#stripendefined)
- [License](#license)

## API

### `assert`

```ts
export function assert(condition: unknown, message?: string): asserts condition {
  if (!condition) {
    throw new Error(message ?? "assertion failed")
  }
}
```

### `signalInvalidType`

```ts
export function signalInvalidType(type: never): never {
  console.error(type)
  throw new TypeError("internal error: invalid type")
}
```

### `mapEntries`

```ts
export const mapEntries = <K extends string, S, T>(object: Record<K, S>, map: (entry: [key: K, value: S]) => T) =>
  Object.fromEntries(Object.entries<S>(object).map(([key, value]) => [key, map([key as K, value])])) as Record<K, T>
```

### `mapKeys`

```ts
export const mapKeys = <K extends string, S, T>(object: Record<K, S>, map: (key: K) => T) =>
  Object.fromEntries(Object.entries<S>(object).map(([key, value]) => [key, map(key as K)])) as Record<K, T>
```

### `mapValues`

```ts
export const mapValues = <K extends string, S, T>(object: Record<K, S>, map: (value: S) => T) =>
  Object.fromEntries(Object.entries<S>(object).map(([key, value]) => [key, map(value)])) as Record<K, T>
```

### `zip`

```ts
export type Zip<E> = E extends Iterable<any>[] ? { [k in keyof E]: E[k] extends Iterable<infer T> ? T : E[k] } : never

export const zip = <E extends Iterable<any>[]>(...args: E): Iterable<[...Zip<E>, number]>
```

### `replaceUndefined`

```ts
/** Recursively replace every `undefined` with `null` in ararys and objects */
export function replaceUndefined(value: JSValue, inPlace = false): JSValue
```

### `stripUndefined`

```ts
/** Recursively remove every object entry with value `undefined` */
export function stripUndefined(value: JSValue, inPlace = false): JSValue
```

## License

MIT © Canvas Technologies, Inc.
