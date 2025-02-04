---
title: getter-return
rule_type: problem
handled_by_typescript: true
further_reading:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get
- https://leanpub.com/understandinges6/read/#leanpub-auto-accessor-properties
---



The get syntax binds an object property to a function that will be called when that property is looked up. It was first introduced in ECMAScript 5:

```js
const p = {
    get name(){
        return "nicholas";
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        return 17;
    }
});
```

Note that every `getter` is expected to return a value.

## Rule Details

This rule enforces that a return statement is present in property getters.

Examples of **incorrect** code for this rule:

::: incorrect

```js
/*eslint getter-return: "error"*/

const p = {
    get name(){
        // no returns.
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        // no returns.
    }
});

class P{
    get name(){
        // no returns.
    }
}
```

:::

Examples of **correct** code for this rule:

::: correct

```js
/*eslint getter-return: "error"*/

const p = {
    get name(){
        return "nicholas";
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        return 18;
    }
});

class P{
    get name(){
        return "nicholas";
    }
}
```

:::

## Options

This rule has an object option:

* `"allowImplicit": false` (default) disallows implicitly returning `undefined` with a `return` statement.

Examples of **correct** code for the `{ "allowImplicit": true }` option:

::: correct

```js
/*eslint getter-return: ["error", { allowImplicit: true }]*/
const p = {
    get name(){
        return; // return undefined implicitly.
    }
};
```

:::

## When Not To Use It

If your project will not be using ES5 property getters you do not need this rule.
