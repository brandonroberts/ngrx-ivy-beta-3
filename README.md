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