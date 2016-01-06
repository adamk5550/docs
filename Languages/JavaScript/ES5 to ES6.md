# Javascript ES5 to ES6

*How to not immediately fail code review in 2016*

## Contents

- [Introduction](#introduction)
- [ES6 Patterns Replacing ES5 Patterns](#es6-patterns-replacing-es5-patterns)
  - [Variable Scope](#variable-scope)
- [New Patterns for ES6](#new-patterns-for-es6)

## Introduction

The 6th edition of ECMAScript, "Harmony" was agreed upon in June 2015. JavaScript uses ECMAScript as its language specification, so this new standard means sweeping changes to the way we use and write JavaScript.

Now that Newcastle Mobility's Hybrid capability is established, it's the perfect time to move with the times and transition from ES5 to ES6.

This is particularly important as the big web libraries: AngularJS, ReactJS and Node.js are all moving in this direction, with big releases expected in 2016.

This guide is designed to show you exactly how coding with ES6 is different to ES5 and highlight how your coding habits will change as a result.

## ES6 Patterns Replacing ES5 Patterns

In this section you'll find all of the ES5 design patterns you're currently using that have changed in ES6.

**Note:** Failure to adopt to these changes will see your code fail code review!

### Variable Scope

In ES5 using `var` before variables is encouraged as it makes the variable *function scoped* rather than *global scoped*.

ES6 introduces two new variable types, `let` and `const`. Both of these are *block scoped*. This means that when declared inside a block, the variable will cease to exist when the block terminates.

`const` is to be used for any variable declaration that is not expected to change, such as an IP address. Although it will not complain when you try, the value of a `const` cannot be changed.

**Usage:** Use `const` for variables that won't change, otherwise use `let`. Only use `var` when a variable absolutely needs to be *function scoped*.

```javascript
// ES5 - Before
var name = 'John';
var sum  = price + vat;

// ES6 - After
const name = 'John';
let sum = price + vat;
```

## New Patterns for ES6

In this section you'll find new design patterns that have been introduced with ES6. They allow new ways of solving problems and should be considered going forward.
