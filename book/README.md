## First Iteration (None Spellchecked written by a german hustler)

## Diffrence between the function keyword and => fat arrow functions
Its importent to understand that functions created with the function keyword do create a scope with a so called this property which should get avoided anyway to keep the code PURE which is nice for performance and modularity as also readability you almost never want to use the function keyword
only exempt you do low level stuff with your Engine in a CJS context to shim the Environment or BootStrap Environments like Electron. 


## type assertions (Typecast)

In TypeScript, you can do const assertions. via writting const after a literal.
```ts
// type is { prop: string }
let a = { prop: "hello" };

// type is { readonly prop: "hello" }
let b = { prop: "hello" } as const;
```

In Stealify/ECMAScript/JavaScript files, you use type assertions to achieve the same thing.
```ts
// type is { prop: string }
let a = { prop: "hello" };

// type is { readonly prop: "hello" }
let b = /** @type {const} */ ({ prop: "hello" });
```

type assertions comments start with ```/** @type {TheTypeWeWant} */``` and are followed by a parenthesized expression ```(someExpression)```
this is also often referenced as Typecasting.
```ts
/** @type {TheTypeWeWantTypecast} */ (someExpression)
```

## default type arguments 

in TypeScript:
```ts
type Foo<T extends string | number = number> = { prop: T };
```

can be rewritten as the following @typedef declaration in JavaScript:
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
