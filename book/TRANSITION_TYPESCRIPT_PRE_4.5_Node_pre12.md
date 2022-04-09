## There has been a Hard deprecation
It was unintendeed but it leads to something good so this is the transition path

create a folder structure to translate pre node12 packages without exports to packages with correct exports. and switch to moduleResolution node12 if you need to work with npm packages

here are some translation examples

## Dual Package 
this is the most complicated situation and should get avoided by repackaging into 2 seperated version or even only offer a ESM version that can get transpiled down to CJS.

./packages/module_name/package.json
```
{ 
  dependencies: {
    "dep-without-exports": "npm:dep@1.0.0"
  },
  exports: {
    "import": "./dep.mjs",
    "require": "./dep.cjs",
  }
}
```

in the above example typescript will lookup ./dep.d.mts and ./dep.d.cts this is needed if you got diffrent types for both files if you got the same types for both files for example when u used the Stealify Module Standard and used only namedExports you can add a types fild above!
how ever that should be avoided as typescript can not link to the correct file via the d.ts.map in a editor when require or import is used so u loose all benefits
```
{ 
  dependencies: {
    "dep-without-exports": "npm:dep@1.0.0"
  },
  exports: {
    "types": "./dep.d.ts",
    "import": "./dep.mjs",
    "require": "./dep.cjs",
  }
}
```

the most best is to create a @esm and @cjs scope inside your node_modules and put your packages there as single package wrappers. containing only a single export via exports: 
```
  "name": "@esm/module_name",
  "version": "",
  "main": "./main.js",
  "type": "module",
  "types": "./main.d.ts",
  "exports": "./main.js"
```
the above example has more wide compatible metadata while it does not get confused as it has only a single export you could avoud all that wrapping when referencing directly a file path on import and when there is a correct dts it gets
picked up if not you simply create a importing wrapper.js file that references the correct .d.ts this way even bundlers can pick that up 

here we use ```/// <reference path="" />, /// <reference types="" />, or /// <reference lib="" />```

./packages/module_name/module.js
```
/// <reference types="node_modules/module_name/types.d.ts" />
export * from 'node_modules/module_name/main.js'
```
or we use a dummy .d.ts that is the most save way and should be the default if you want to magic import that construct create the following

./packages/module_name/module.d.ts
```ts
export * from 'node_modules/module_name/types.d.ts'
```

## Final Conclusion
Avoid Packages as dependencies prefer modules over packages create modules from your packages that you depend on. consider releasing the repackaged modules.
