# NgRx and Ivy

This repo shows NgRx failing to run with Angular Ivy and the latest betas.

## Reproduction Steps

- Clone the repo
- Install the dependencies

```sh
yarn
```

- Run the app

```
yarn start --aot
```

- Note that the app compiles successfully
- Browse to `http://localhost:4200`
- Note that the app fails at runtime with the error

```
main.ts:13 Error: Dependency array must have arguments.
    at reflectDependency (core.js:887)
    at core.js:870
    at Array.map (<anonymous>)
    at convertDependencies (core.js:870)
    at reflectDependencies (core.js:866)
    at Function.get (core.js:956)
    at getInjectableDef (core.js:312)
    at injectableDefOrInjectorDefFactory (core.js:13259)
    at providerToFactory (core.js:13297)
    at providerToRecord (core.js:13281)
```

Fix:

Add `import 'core-js/es7/reflect';` to `src/polyfills.ts`

- Run the app in prod mode

```
yarn start --prod
```

- Note the app fails at runtime with the error

```
Error: Angular JIT compilation failed: '@angular/compiler' not loaded!
  - JIT compilation is discouraged for production use-cases! Consider AOT mode instead.
  - Did you bootstrap using '@angular/platform-browser-dynamic' or '@angular/platform-server'?
  - Alternatively provide the compiler with 'import "@angular/compiler";' before bootstrapping.
    at Ae (core.js.pre-build-optimizer.js:448)
    at Ge (core.js.pre-build-optimizer.js:869)
    at ze (core.js.pre-build-optimizer.js:866)
    at Function.get (core.js.pre-build-optimizer.js:20742)
    at ge (core.js.pre-build-optimizer.js:320)
    at e.processInjectorType (core.js.pre-build-optimizer.js:13161)
    at core.js.pre-build-optimizer.js:13179
    at core.js.pre-build-optimizer.js:13340
    at Array.forEach ()
    at va (core.js.pre-build-optimizer.js:13340)
```

Fix:

Disable `buildOptimizer` in the `angular.json` file