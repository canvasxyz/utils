# @canvas-js/utils

[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg)](https://github.com/RichardLitt/standard-readme) [![license](https://img.shields.io/github/license/canvasxyz/utils)](https://opensource.org/licenses/MIT) [![NPM version](https://img.shields.io/npm/v/@canvas-js/utils)](https://www.npmjs.com/package/@canvas-js/utils) ![TypeScript types](https://img.shields.io/npm/types/@canvas-js/utils)

This repo is for utility methods and types related to JavaScript programming in general.

Anything that is only used by a single package should go in that package's src/utils.ts file; and anything that is related to a specific feature or domain should go in its own utility package.

## Table of contents

- [API](#api)
  - [`assert`](#assert)
  - [`Awaitable`](#awaitable)
  - [`JSONValue`](#jsonvalue)
  - [`JSValue`](#jsvalue)
  - [`deepEqual`](#deepequal)
  - [`mapEntries`](#mapentries)
  - [`mapKeys`](#mapkeys)
  - [`mapValues`](#mapvalues)
  - [`replaceUndefined`](#replaceendefined)
  - [`stripUndefined`](#stripendefined)
  - [`signalInvalidType`](#signalinvalidtype)
  - [`zip`](#zip)
- [License](#license)

## API

### `assert`

```ts
export function assert(condition: unknown, message?: string): asserts condition
```

### `Awaitable`

```ts
export type Awaitable<T> = T | Promise<T>
```

### `JSONValue`

```ts
export type JSONValue =
  | null
  | boolean
  | number
  | string
  | JSONArray
  | JSONObject

export interface JSONArray extends Array<JSONValue> {}
export interface JSONObject {
  [key: string]: JSONValue
}
```

### `JSValue`

```ts
export type JSValue =
  | undefined
  | null
  | boolean
  | number
  | string
  | Uint8Array
  | JSArray
  | JSObject

export interface JSArray extends Array<JSValue> {}
export interface JSObject {
  [key: string]: JSValue
}

export function isArray(value: JSValue): value is JSArray
export function isObject(value: JSValue): value is JSObject

export type JSType =
  | "undefined"
  | "null"
  | "boolean"
  | "number"
  | "string"
  | "Uint8Array"
  | "Array"
  | "Object"

export function typeOf(value: JSValue): JSType
```

### `deepEqual`

```ts
export function deepEqual(a: JSValue, b: JSValue): boolean
```

### `mapEntries`

```ts
export function mapEntries<K extends string, S, T>(
  object: Record<K, S>,
  map: (entry: [key: K, value: S]) => T,
): Record<K, T>
```

### `mapKeys`

```ts
export function mapKeys<K extends string, S, T>(
  object: Record<K, S>,
  map: (key: K) => T,
): Record<K, T>
```

### `mapValues`

```ts
export function mapValues<K extends string, S, T>(
  object: Record<K, S>,
  map: (value: S) => T,
): Record<K, T>
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

### `signalInvalidType`

```ts
export function signalInvalidType(type: never): never
```

### `zip`

```ts
export type Zip<E> = E extends Iterable<any>[]
  ? { [k in keyof E]: E[k] extends Iterable<infer T> ? T : E[k] }
  : never

export function zip<E extends Iterable<any>[]>(
  ...args: E
): Iterable<[...Zip<E>, number]>
```

## License

MIT © Canvas Technologies, Inc.
