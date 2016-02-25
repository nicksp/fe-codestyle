# ECMAScript 6 Style Guide

This section describes code style for [ECMAScript® 2015 Language Specification](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

## Table of Contents

  1. [Strict Mode](#strict-mode)
  1. [Variable Declaration](#variable-declaration)
  1. [Classes](#classes)
  1. [Arrow Functions](#arrow-functions)
  1. [Objects](#objects)
  1. [Template Strings](#template-strings)
  1. [Destructuring](#destructuring)
  1. [Default Parameters](#default-parameters)
  1. [Rest Parameters](#rest-parameters)
  1. [Spread Operator](#spread-operator)
  1. [Generators](#generators)
  1. [Modules](#modules)

## Strict Mode

- [Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) should be used.

  > Explanation:
  > - It prevents nasty [bugs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode#Changes_in_strict_mode).
  > - Many useful features of language (e.g. [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [let declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [block scopes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Block_scope_with_let)) are available only in strict mode.
  > - It simplifies migration to [ECMAScript modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/),
  because they are always in strict mode by default.

- The strict mode directive should be followed by a blank line.

- Strict mode should be enabled explicitly using the `'use strict'` directive.

  > Explanation:
  > - Dependencies of your code may not work in strict mode.
  > - Your code can be used in non-strict mode.

  ```js
  // Good
  'use strict';

  console.log('a proper way of declaring strict mode');
  ```

**[⬆ back to TOC](#table-of-contents)**

## Variable Declaration

- Avoid using `var`.
- All immutable references should be declared using a [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const).
- [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) should be used only for mutable references
(i.e. when variable might be (re)assigned different value later in the code)

  ```js
  // Bad

  // Reader expects count to change!
  let count = observers.length;
  let index = 0;
  while (index < count) {
    const observer = observers[index];
    observer(...args);
    index += 1;
  }

  const count = observers.length;
  let index = 0;
  while (index < count) {
    // Reader expects observer to change within the block!
    let observer = observers[index];
    observer(...args);
    index += 1;
  }

  const count = observers.length;
  // Do not use `var`
  var index = 0;
  while (index < count) {
    observers[index](...args);
    index += 1;
  }

  // Good
  const count = observers.length;
  let index = 0;
  while (index < count) {
    const observer = observers[index];
    observer(...args);
    index += 1;
  }
  ```

- If the reference is immutable, but the value is mutable, `const` declaration should be used:

  ```js
  // Bad
  let person = {};
  person.name = 'Nick';

  // Good
  const person = {};
  person.name = 'Nick';
  ```

- Remember that both `let` and `const` are block-scoped.

  ```js
  {
    let a = 1;
    const b = 1;
  }

  console.log(a); // ReferenceError
  console.log(b); // ReferenceError
  ```

**[⬆ back to TOC](#table-of-contents)**

## Classes

- For class definition the `class` keyword should be used. Avoid manipulating `prototype` directly:

  ```js
  // Bad
  function Circle(x, y, radius) {
    this.x = x;
    this.y = y;
    this.radius = radius;
  }

  Circle.prototype.area = function () {
    return Math.PI * Math.pow(this.radius, 2);
  };

  // Good
  class Circle {
    constructor(x, y, radius) {
      this.x = x;
      this.y = y;
      this.radius = radius;
    }

    area() {
      return Math.PI * Math.pow(this.radius, 2);
    }
  }
  ```

- There should be one whitespace after the class name:

  ```js
  // Bad
  class Circle{}

  // Good
  class Circle {}
  ```

- There should be no whitespace after method name:

  ```js
  // Bad
  class Circle {
    area () {}
  }

  // Good
  class Circle {
    area() {}
  }
  ```

- There should be one whitespace before the opening curly brace of method's body:

  ```js
  // Bad
  class Circle {
    area(){}
  }

  // Good
  class Circle {
    area() {}
  }
  ```

- The constructor (if exists) should be the first method in a class definition:

  ```js
  // Bad
  class Circle {
    area() {}

    constructor() {}
  }

  // Good
  class Circle {
    constructor() {}

    area() {}
  }
  ```

- For inheritance the `extends` keyword should be used.

  > Explanation:
  > - It is a built-in way to inherit prototype functionality without breaking `instanceof`.

  ```js
  // Bad
  const module = require('module');

  class Stream() {
    constructor() {
      EventEmitter.call(this);
    }
  }

  module.inherits(Stream, EventEmitter);

  // Good
  class Stream extends EventEmitter {}
  ```

- Methods can return `this` to help with method chaining.

  ```js
  const classInst = new ClassInst();

  classInst.method1()
    .method2()
    .method3();
  ```

**[⬆ back to TOC](#table-of-contents)**

## Arrow Functions

- [Arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
  should be used where an anonymous function is expected (when you need function and you don't want bind it to an
  identifier) or even when exporting function from ES6 module:

  > Explanation: Arrow functions capture the `this` value of the enclosing context. That prevents run-time errors with
  > unexpected values of `this`. Also it's a more efficient method than binding `this` value using
  > `Function.prototype.bind`.

  ```js
  [1, 2, 3].map((x) => {
      // ...
  });

  // Use `function` here, because we're passing `ctx` as `this` argument.
  [1, 2, 3].map(function (x) {
      // ...
  }, ctx);
  ```

- Always add parentheses around arrow function parameters:

  > Explanation:
  > - This style is consistent with cases when function takes zero or more than one parameters.
  > - You need to alter the code less times, if the number of parameters changes.

  ```js
  // Bad
  [1, 2, 3].map(x => x * 2);

  // Good
  [1, 2, 3].map((x) => x * 2);
  [1, 2, 3].reduce((i, n) => i + n);
  ```

- Before and after an arrow function's fat arrow (`=>`) whitespace is required:

  ```js
  // Bad
  [1, 2, 3].map((x)=> x * 2);

  // Good
  [1, 2, 3].map((x) => x * 2);
  ```

- If the function body consists of a single expression, braces should be omitted and implicit return should be used:

  ```js
  // Bad
  [1, 2, 3].map((x) => { return x * 2; });

  // Good
  [1, 2, 3].map((x) => x * 2);
  ```

- Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`).

  ```js
  // Bad
  let x = a => 1 ? 2 : 3

  // Good
  let x = (a) => { return a >= 1 ? 2 : 3; }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Objects

- Use object method shorthand.

  ```js
  // Bad
  const obj = {
    value: 1,

    addValue: function (value) {
      return obj.value + value;
    }
  };

  // Good
  const obj = {
    value: 1,

    addValue(value) {
      return obj.value + value;
    }
  };
  ```

- Use property value shorthand.

  ```js
  const language = 'JavaScript';

  // Bad
  const obj = {
    language: language
  };

  // Good
  const obj = {
    language
  };
  ```

- Use computed property names for objects, if such names are supposed to be dynamic.

  > Explanation:
  > - They allow you to define all the properties of an object in one place.

  ```js
  function getKey(k) {
    return `a key named ${k}`;
  }

  // bad
  const obj = {
    id: 7,
    name: 'Stockholm'
  };
  obj[getKey('enabled')] = true;

  // Good
  const obj = {
    id: 7,
    name: 'Stockholm',
    [getKey('enabled')]: true
  };
  ```

**[⬆ back to TOC](#table-of-contents)**

## Template Strings

- When programmatically building up strings, use template strings instead of concatenation.
- Spaces in placeholders (between `${` and `}`) should not be used:

  ```js
  // Bad
  `Hello ${ name }`

  // Good
  `Hello ${name}`
  ```

**[⬆ back to TOC](#table-of-contents)**

## Destructuring

- Use object destructuring.

  ```js
  // Bad
  function getFullName(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;
    return `${firstName} ${lastName}`;
  }

  // Good
  function getFullName(user) {
    const { firstName, lastName } = user;
    return `${firstName} ${lastName}`;
  }

  // Best
  function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
  }
  ```

- Use array destructuring.

  ```js
  const arr = [1, 2, 3, 4];

  // Bad
  const first = arr[0];
  const second = arr[1];

  // Good
  const [first, second] = arr;
  ```

**[⬆ back to TOC](#table-of-contents)**

## Default Parameters

- Instead of mutating function arguments use default parameters.

  ```js
  // Bad
  function decorateElement(options) {
    options = options || {};
    // the rest of the code
  }

  // Good
  function decorateElement(options = {}) {
    // the rest of the code
  }
  ```

- Always put default parameters last. So that they could easily be skipped during function invocation.

  ```js
  // Bad
  function decorateElement(options = {}, param) {
    // the rest of the code
  }

  // Good
  function decorateElement(param, options = {}) {
    // the rest of the code
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Rest Parameters

- Never use arguments, opt to use rest syntax `...` instead. It allows you to store trailing arguments in a real array.

  ```js
  // Bad
  function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
  }

  // Good
  function doSomething(x, ...remaining) {
     return x * remaining.length;
  }

  doSomething(5, 0, 0, 0); // 15
  ```

**[⬆ back to TOC](#table-of-contents)**

## Spread Operator

- Use array spreads `...` to expand elements of an array in specific places, such as arguments in function calls. Or, it can be applied to all iterable objects, such as a `NodeList`:

  ```js
  // Good
  let values = [1, 2, 4];
  let some = [...values, 8]; // [1, 2, 4, 8]
  let more = [...values, 8, ...values]; // [1, 2, 4, 8, 1, 2, 4]

  const values = [1, 2, 4];

  // Bad
  doSomething.apply(null, values);

  // Good
  doSomething(...values);

  // Good
  let form = document.querySelector('#my-form'),
     inputs = form.querySelectorAll('input'),
     selects = form.querySelectorAll('select');

  let allTheThings = [form, ...inputs, ...selects];
  ```

**[⬆ back to TOC](#table-of-contents)**

## Generators

- The asterisk `*` in a [generator declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*) should be sticked to the `function` keyword:

  ```js
  // Bad
  function *createIterator() {
    yield 1;
  }

  const createIterator = function * () {
    yield 1;
  };

  // Good
  function* createIterator() {
    yield 1;
  }

  const createIterator = function* () {
    yield 1;
  };
  ```

- In a [shorthand method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions) the asterisk should be sticked to the `method name`:

  ```js
  // Bad
  class Graph {
    * edges() {}
  }

  // Good
  class Graph {
    *edges() {}
  }
  ```

- In a [yield* expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield*) the asterisk should be sticked to the `yield` keyword:

  **Good:**

  ```js
  // Bad
  function* gen() {
    yield *anotherGen();
  }

  // Good
  function* gen() {
    yield* anotherGen();
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Modules

- Try to always use ES6 native module syntax over other sorts of module systems (like AMD or CommonJS). Modules are designed around the `export` and `import` keywords:

  ```js
  // lib/math.js
  export function sum(x, y) {
     return x + y;
  }

  export const PI = 3.141593;

  // app.js
  import { sum, PI } from 'lib/math';
  console.log('2π = ' + sum(PI, PI));
  ```

- Do not export directly from an import.

  > Explanation:
  > - Although the one-liner is concise, having one clear way to `import` and one clear way to `export` makes things consistent.

  ```js
  // Bad
  // es6.js
  export { es6 as default } from './app';

  // Good
  // es6.js
  import { es6 } from './app';
  export default es6;
  ```

**[⬆ back to TOC](#table-of-contents)**
