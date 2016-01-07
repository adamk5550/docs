# Javascript ES5 to ES6

*How to not immediately fail code review in 2016*

## Contents

- [Introduction](#introduction)
- [ES6 Patterns Replacing ES5 Patterns](#es6-patterns-replacing-es5-patterns)
  - [Variable Scope](#variable-scope)
  - [Object Property Shorthands](#object-property-shorthands)
  - [Template Strings](#template-strings)
  - [Arrow Functions](#arrow-functions)
- [New Patterns for ES6](#new-patterns-for-es6)
  - [Array Spreads](#array-spreads)
  - [Object and Array Destructuring](#object-and-array-destructuring)
  - [Default Arguments](#default-arguments)

## Introduction

The 6th edition of ECMAScript, "Harmony" was agreed upon in June 2015. JavaScript uses ECMAScript as its language specification, so this new standard means sweeping changes to the way we use and write JavaScript.

Now that Newcastle Mobility's Hybrid capability is established, it's the perfect time to move with the times and transition from ES5 to ES6.

This is particularly important as the big web libraries: AngularJS, ReactJS and Node.js are all moving in this direction, with big releases expected in 2016.

This guide is designed to show you exactly how coding with ES6 is different to ES5 and highlight how your coding habits will change as a result.

As before, Newcastle Mobility will be following the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript), but no longer specifically following the ES5 variation.

## ES6 Patterns Replacing ES5 Patterns

In this section you'll find all of the ES5 design patterns you're currently using that have changed in ES6.

**Note:** Failure to adopt to these changes will see your code fail code review!

### Variable Scope

In ES5 using `var` before variables is encouraged as it makes the variable *function scoped* rather than *global scoped*.

ES6 introduces two new variable types, `let` and `const`. Both of these are *block scoped*. This means that when declared inside a block, the variable will cease to exist when the block terminates.

`const` is to be used for any variable declaration that is not expected to change, such as an IP address. Although it will not complain when you try, the value of a `const` cannot be changed.

**Usage:** Use `const` for variables that won't change, otherwise use `let`. Only use `var` when a variable absolutely needs to be *function scoped*. Group `const` and `let` declarations for readability.

```javascript
// ES5 - Before
var name  = 'Tomatoes';
var price = 0.4;
price = 0.45;

// ES6 - After
const name  = 'Tomatoes';
let price = 0.4;
price = 0.45;
```

### Object Property Shorthands

In ES5 you have to be explicit when naming object properties when creating a new object. This includes properties created from variables of the same name, and function properties.

ES6 introduces some readable shortcuts for both of these property declarations:

* If a property and variable share the same name, omit the property name. Group these at the top of the object.
* When defining a function property, name the function and omit the property name.

```javascript
// ES5 - Before
var name = 'John';
var person = {
  name: name,
  talk: function() {
    console.log('Hello!');
  }
};

// ES6 - After
const name = 'John';
const person = {
  name,
  function talk() {
    console.log('Hello!');
  }
};
```

### Template Strings

Concatenating (joning together) strings in ES5 can be a chore, usually involving lots of `+` operators. Occasionally you'll come across some code where someone has got sick of this and instead assembled an array and used `Array.join()` on it, or worse, used `Array.concat()`. It can get messy.

Thankfully ES6 has came to our rescue and provided a much simpler (and shorter) way of constructing strings. Template strings use interpolation to achieve the same goal in a much more elegant way:

```javascript
const name = 'Fluffy';
const food = 'fish';

// ES5 - Before
var sentence = 'My cat is called ' + name + '. ' + name + ' likes ' + food + '!';

// ES6 - After
const sentence = `My cat is called ${name}. ${name} likes ${food}!`;
```

It should be noted that anything inside of the braces in a template string is evaluated as normal JavaScript, so anything such as object/array references and operators can be used.

### Arrow Functions

The usual way of defining anonymous functions in ES5 is changing dramatically in favour of ES6's more succinct format. Arrow functions do away with the word `function` appearing frequently, but also have the added benefit of executing the function in the context of `this`, which can be useful depending on what you're doing.

Arrow functions start by defining the function arguments in the usual round brackets, followed by an arrow (or rocket) `=>` and the usual function block:

```javascript
const breeds = ['siamese', 'persian', 'bengal', 'manx'];

// ES6 - Before
breeds.sort(function(a, b) { ... });

// ES6 - After
breeds.sort((a, b) => { ... });
```

When the arrow function only has one argument, omit the surrounding brackets:

```javascript
breeds.forEach(breed => { console.log(breed); });
```

## New Patterns for ES6

In this section you'll find new design patterns that have been introduced with ES6. They allow new ways of solving problems and should be considered going forward.

### Array Spreads

*As of Node.js 5.3.0 the `--harmony` option is required to use this feature.*

When declaring a function it is now possible to capture a variable number of arguments as an array. This is particularly useful when you're not sure how many arguments to expect, or want to allow the function to work with any number of arguments.

There are ways of achieving this in ES5 but they're not pretty: the `arguments` object can be converted into an array of values, or an array can be directly passed to the function. Array spreads are much more elegant:

```javascript
const printLines = function printLines(...lines) {
  lines.forEach(line => {
    console.log(line);
  });
}

printLines('Hello world!');
printLines('Carrots', 'Broccoli', 'Tomatoes');
```
```
Hello world!
Carrots
Broccoli
Tomatoes
```

Array spreads can also be used for concatenating multiple arrays together in more complex ways than `Array.concat()` allows (although this should always be used where practical):

```javascript
const small = [1, 2, 3];
const large = [5, 6, 7];
const all = [...small, 4, ...large];
```
```javascript
[ 1, 2, 3, 4, 5, 6, 7 ]
```

Array spreads are now also the standard way of making a copy of an array, remembering that arrays are normally *pass by reference*:

```javascript
const arrayCopy = [...originalArray];
```

### Object and Array Destructuring

*As of Node.js 5.3.0 the `--harmony_destructuring` option is required to use this feature.*

ES6 provides a new way of extracting variables from objects and arrays called destructuring. This is much more elegant than writing a variable assignment line per variable, and considerably more readable.

For objects this works by specifying the properties to turn into variables (the key becomes the variable name). For arrays new variable names are specified and the array values are assigned in order.

Note that the variable scope is still defined.

```javascript
const array = ['meow', 'purr', 'hiss'];
const object = { animal: 'cat', colour: 'black', name: 'Whiskers' };

// ES5 - Before
var first = array[0];
var second = array[1];
var name = object.name;
var colour = object.colour;

// Es6 - After
const [ first, second ] = array;
const { name, colour } = object;
```

### Default Arguments

ES6 brings with it support for default arguments for functions. This allows a function to have a defined value that is used only when the function call does not specify another value. This is a long awaited feature as it means we can stop using silly workarounds to use this functionality:

```javascript
// ES5 - Before
var outputMessage = function outputMessage(message) {
  var message = message || 'No message!';
  console.log(message);
};

// ES6 - After
const outputMessage = function outputMessage(message = 'No message!') {
  console.log(message);
};
```
