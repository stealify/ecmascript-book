## First Iteration (None Spellchecked written by a german hustler)


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
or
```ts
/**
 * @template {string | number} [T=number]
 * @typedef {{ prop: T }} Foo
 */
 ```
