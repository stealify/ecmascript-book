## First Iteration (None Spellchecked written by a german hustler)

## Preamble
- Stealify always references to Stealify / ECMAScript / JavaScript so .js files


## Create Raw Objects
This is used to avoid collissions between prototype keys and implementations as also to save overhead when enum 
```
const rawObjectToStoreData = Object.create(null); // has no methods assigned to it!
```
usage of such an object
```
const { toString, hasOwnProperty } = Object.prototype;
toString.call(rawObjectToStoreData);
hasOwnProperty.call(rawObjectToStoreData, 'prop')
```

## Diffrence between the function keyword and => fat arrow functions
Its importent to understand that functions created with the function keyword do create a scope with a so called this property which should get avoided anyway to keep the code PURE which is nice for performance and modularity as also readability you almost never want to use the function keyword
only exempt you do low level stuff with your Engine in a CJS context to shim the Environment or BootStrap Environments like Electron. 


## type assertions (Typecast)

In TypeScript, you can do const assertions. via writting const after a literal. example.ts
```ts
// type is { prop: string }
let a = { prop: "hello" };

// type is { readonly prop: "hello" }
let b = { prop: "hello" } as const;
```

In Stealify / ECMAScript / JavaScript files, you use type assertions to achieve the same thing. example.js
```ts
// type is { prop: string }
let a = { prop: "hello" };

// type is { readonly prop: "hello" }
let b = /** @type {const} */ ({ prop: "hello" });
```

type assertions comments start with ```/** @type {TheTypeWeWant} */``` and are followed by a parenthesized expression ```(someExpression)```
this is also often referenced as Typecasting. example.js
```ts
/** @type {TheTypeWeWantTypecast} */ (someExpression)
```

## default type arguments 

in TypeScript: example.ts
```ts
type Foo<T extends string | number = number> = { prop: T };
```

can be rewritten as the following @typedef declaration in Stealify / ECMAScript / JavaScript: example.js
```ts
/**
 * @template {string | number} [T=number]
 * @typedef Foo
 * @property prop {T}
 */
```
or less verbose
```ts
/**
 * @template {string | number} [T=number]
 * @typedef {{ prop: T }} Foo
 */
 ```
