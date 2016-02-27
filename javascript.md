# JavaScript Style Guide

I tend to describe it as a clear, concise and predictable approach to writing my own JavaScript code.

## Table of Contents

  1. [General Formatting](#general-formatting)
  1. [Strict Mode](#strict-mode)
  1. [Semicolons](#semicolons)
  1. [Commas](#commas)
  1. [Naming](#naming)
  1. [Variable Declaration](#variable-declaration)
  1. [Literals](#literals)
      - [Objects](#objects)
      - [Arrays](#arrays)
      - [Strings](#strings)
  1. [Functions](#functions)
  1. [Keywords](#keywords)
  1. [Block Statements](#block-statements)
  1. [Conditional Statements](#conditional-statements)
      - [if](#if)
      - [switch](#switch)
  1. [Loops](#loops)
      - [for](#for)
      - [for..in)](#for--in)
  1. [Operators](#operators)
      - [with](#with)
      - [Comparison Operators](#comparison-operators)
      - [Ternary Operator](#ternary-operator)
      - [Unary Operators](#unary-operators)
  1. [eval](#eval)
  1. [undefined](#undefined)
  1. [Parentheses](#parentheses)
  1. [Exceptions](#exceptions)
  1. [Type Casting](#type-casting)
  1. [Multi-Line Statements](#multi-line-statements)
  1. [Method Chaining](#method-chaining)
  1. [String Concatenation](#string-concatenation)
  1. [Empty Lines](#empty-lines)
  1. [Function Context](#function-context)
  1. [Comments](#comments)
  1. [Classes](#classes)
  1. [Enums](#enums)
  1. [Events](#events)
  1. [jQuery](#jquery)
  1. [Testing](#testing)
  1. [Performance](#performance)
  1. [Resources](#resources)

## General Formatting

- Files should be encoded in UTF-8 without [BOM](http://en.wikipedia.org/wiki/Byte-order_mark).
- Use UNIX-like line-break character `LF` - `\n`.
- Files should end with a `LF` character.
- One level of indentation is achieved with 2 spaces. Spaces are the only way to guarantee code renders the same in any person’s environment and improve readability. Always be consistent in your use of whitespace. Never mix them with tabs.
- Clean up any trailing whitespace at the end of lines in your JS files before committing. Trailing whitespace is unnecessary and can complicate diffs.

  ***Pro tip:*** use an [EditorConfig](http://editorconfig.org/) file (or equivalent) to help maintain the basic whitespace conventions that have been agreed for your code-base. For an example, see [the one in my Redux boilerplate](https://github.com/nicksp/redux-webpack-es6-boilerplate/blob/extended/.editorconfig).

- Lines should be no longer than 120 characters.

**[⬆ back to TOC](#table-of-contents)**

## Strict Mode

- The first line of every file should be `'use strict';`. If the file contains a shebang, strict mode should be enabled on the second line.
- The strict mode directive should be followed by a blank line.

  ```js
  // Bad
  'use strict';
  console.log('even when not required')

  // Good

  // 1
  'use strict';

  console.log('even when not required');

  // 2
  #!/usr/bin/env node
  'use strict';

  // Code goes here
  ```

**[⬆ back to TOC](#table-of-contents)**

## Semicolons

- Statements should always end with a semicolon `;`

  ```js
  // Bad
  console.log('even when not required')

  // Good
  console.log('even when not required');
  ```

**[⬆ back to TOC](#table-of-contents)**

## Commas

- Never begin a line with `,` (always at the end of the previous line).
- No additional trailing commas. This can cause problems with IE6/7 and IE9 if it's in quirksmode.

  ```js
  // Bad
  execute('some error message'
    , 12345
    , this);

  var obj = {
      prop1: val1
    , prop2: val2
    , prop3: val3
  };

  // Good
  execute('some error message',
    12345,
    this);

  var obj = {
    prop1: val1,
    prop2: val2,
    prop3: val3
  };
  ```

**[⬆ back to TOC](#table-of-contents)**

## Naming

- `variableNamesLikeThis`
- `functionNamesLikeThis`
- `functionArgumentsLikeThis`
- `ClassNamesLikeThis`
- `EnumNamesLikeThis`
- `methodNamesLikeThis`
- `CONSTANTS_LIKE_THIS`
- `namespacesLikeThis`
- `events-like-this`
- `private` or `protected` properties and methods should be prefixed with a single `_` character
- Shortened and abbreviated names should be avoided.
- Common abbreviations, such as `JSON` and `XML` are written in `CamelCase`. For example: `Json`, `Xml`, etc.

**[⬆ back to TOC](#table-of-contents)**

## Variable Declaration

- Each variable should be declared:
  * using a `var` statement (ES5);
  * using `let` and `const` (ES6);
  * only once in the current scope;
  * on a new line;
  * as close as possible to the place where it's first used.

- Give descriptive names:
  * `for...in`, `for...of` iterators should use descriptive names;
  * `for` iterators should use single character names;
  * Use combination of plural for array and singular for each item in the array.

- Each `var` statement should have only one variable declared in it.

  ```js
  // Bad
  var keys = ['foo', 'bar'],
      values = [23, 42],
      object = {},
      key;

  while (items.length) {
    key = keys.pop();
    object[key] = values.pop();
  }

  // Good
  var keys = ['foo', 'bar'];
  var values = [23, 42];

  var object = {};
  while (items.length) {
    var key = keys.pop();
    object[key] = values.pop();
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Literals

### Objects

- Add spaces inside curly braces `{` and `}`.
  * No space for empty objects `{}`.

  ```js
  // Bad
  var obj = {a: 1, b: 2, c: 3};
  this.method({a: 1, b: 2});
  var empty = { };

  // Good
  var obj = { a: 1, b: 2, c: 3 };
  this.method({ a: 1, b: 2 });
  var empty = {};
  ```

- There should be no whitespace characters before the colon.

  ```js
  // Bad
  let obj = {
    a : 1,
    b :2,
    c :3
  };

  // Good
  var obj = {
    prop: 0
  };
  ```

- Only property names should be aligned within object literals.

  ```js
  // Bad
  var obj = {
    a          : 0,
    b          : 1,
    lengthyName: 2
  };

  // Good
  var obj = {
    a: 0,
    b: 1,
    lengthyName: 2
  };
  ```

- Quotes around property names should be typed only for invalid identifiers.

  ```js
  // Bad
  var obj = {
    'key': 0,
    'key-key': 1
  };

  // Good
  var obj = {
    key: 0,
    'key-key': 1
  };
  ```

**[⬆ back to TOC](#table-of-contents)**

### Arrays

- When enumerating elements in an array literal, spaces should be typed after the comma only.

  ```js
  var fellowship = ['foo', 'bar', 'baz'];
  ```

**[⬆ back to TOC](#table-of-contents)**

### Strings

- String literals should use single quotes `'` over double quotes `"`.

  ```js
  var lyrics = 'Never gonna give you up. Never gonna let you down.';
  ```

- If a string contains a single quote character, it should be escaped.

  ```js
  var test = 'It shouldn\'t fail';
  ```

- When dealing with multi-line string, follow [these rules](#string-concatenation).

**[⬆ back to TOC](#table-of-contents)**

## Functions

- Write small functions.

  Keep your functions short. A good function fits on a slide that the people in the last row of a big room can comfortably read. So don't count on them having perfect vision and limit yourself to ~15 lines of code per function.
- Proper spacing in a function signature.
  * No space inside curly braces for empty functions `{}`.

  ```js
  // Bad
  const f = function(){};
  const g = function (){};
  const h = function() {};

  // Good
  const x = function () {};
  const y = function a() {};
  ```

- Immediately invoked function expressions (IIFE)

  > Explanation:
  > - An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

  ```js
  // IIFE
  (function () {
    console.log('Welcome to the world.');
  }());
  ```

- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently.
- Never use the Function constructor to create a new function.

  > Explanation:
  > - Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

- Never use the Function constructor to create a new function.

  > Explanation:
  > - Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

  ```js
  // Bad
  var add = new Function('a', 'b', 'return a + b');

  // Still bad
  var subtract = Function('a', 'b', 'return a - b');

  // Good
  var subtract = function subtract(a, b) {
    return a - b;
  }
  ```
- Never mutate or reassing parameters.

  > Explanation:
  > - Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.
  > - Reassigning parameters can lead to unexpected behavior, especially when accessing the arguments object. It can also cause optimization issues, especially in V8.

  ```js
  // Bad
  function f1(a) {
    a = 1;
  }

  function f2(a) {
    if (!a) { a = 1; }
  }

  // Good
  function f3(a) {
    var b = a || 1;
  }

  function f4(a = 1) {}
  ```

**[⬆ back to TOC](#table-of-contents)**

## Keywords

- Keywords are always followed by a single space character.

  ```js
  if (test) {
    // ...
  }

  function foo() {
    // ...
  }

  var bar = function () {
    // ...
  };
  ```

- If the keyword is followed by a semicolon, there should be no space between them.

  ```js
  return;
  ```

**[⬆ back to TOC](#table-of-contents)**

## Block Statements

- The opening curly brace should be on the same line and separated with one space character.

  ```js
  if (test) {
    // ...
  }

  function foo() {
    // ...
  }
  ```

- Branching and looping statements should always be surrounded with curly braces.

  ```js
  // Bad
  if (test)
    return;

  if (test) return;

  if (test) { return; }

  // Good
  if (test) {
    return;
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Conditional Statements

### if

- The `else` keyword should be on the same line as the `if` block's closing brace.

  ```js
  // Bad
  if (test) {
    // ...
  }
  else {
    // ...
  }

  // Good
  if (test) {
    // ...
  } else {
    // ...
  }
  ```

- Condition statements should not contain assignment operations.

  ```js
  // Bad
  var foo;
  if ((foo = bar()) > 0) {
    // ...
  }

  // Good
  var foo = bar();
  if (foo > 0) {
    // ...
  }
  ```

- Logical operators should not be used for conditional branching.

  ```js
  // Bad
  condition && actionIfTrue() || actionIfFalse();

  // Good
  if (condition) {
    actionIfTrue();
  } else {
    actionIfFalse();
  }
  ```

- Conditions longer than the [maximum line length](#general-formatting) should be divided into multiple  lines to improve readability.
- Conditions should be indented to the first character of the condition in the first line.

  ```js
  if (longCondition ||
      anotherLongCondition &&
      yetAnotherLongCondition
  ) {
    console.log('Do like I do.');
  }
  ```

- [Yoda conditions](http://en.wikipedia.org/wiki/Yoda_conditions) should not be used:

  ```js
  // Bad
  if ('driving' === getType()) {
    // ...
  }

  // Good
  if (getType() === 'driving') {
    // ...
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

### switch

The switch statement should be written as in the example.

  ```js
  // Bad
 switch (foo) {
 case 1:
   let x = 1;
   break;
 case 2:
   const y = 2;
   break;
 case 3:
   function f() {}
   break;
 default:
   class C {}
 }

  // Good
  switch (value) {
    case 1:
      // ...
      break;

    case 2:
      // ...
      break;

    default:
      // ...
      // no break keyword on the last case
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Loops

### for

- Usually used with arrays.
- If possible, [Array.prototype.forEach](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) should be used instead of a `for` loop.

  ```js
  [1, 2, 3].forEach(function (value) {
    console.log(value);
  });
  ```
- Performance-critical parts of the code can use a regular `for` loop.

**[⬆ back to TOC](#table-of-contents)**

### for..in

- Should be used for objects.
- If possible, [Object.keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) should be used instead of a `for..in` construction.

  ```js
  Object.keys(obj).forEach(function (key) {
    console.log(key);
  });
  ```

**[⬆ back to TOC](#table-of-contents)**

## Operators

### with

The `with` operator should not be used.

**[⬆ back to TOC](#table-of-contents)**

### Comparison Operators

If there is no need for type casting, the strict equality operator `===` (or strict inequality `!==`) should be used over `==` and `!=`.

**[⬆ back to TOC](#table-of-contents)**

### Ternary Operator

The ternary operator should be written as in the examples.

```js
var x = a ? b : c;

var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

var z = a ?
    moreComplicatedB :
    moreComplicatedC;
```

**[⬆ back to TOC](#table-of-contents)**

### Unary Operators

Unary operators should be typed without whitespace between them and their operands:

```js
var foo = !bar;
```

Exceptions from this rule are the unary [special JS operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Unary_operators), such as `delete`, `typeof`, `void`.

**[⬆ back to TOC](#table-of-contents)**

## eval

The `eval` function should be avoided.
`json` serialized data should be parsed with [JSON.parse](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/JSON/parse).

**[⬆ back to TOC](#table-of-contents)**

## undefined

- Checking for `undefined` value of declared variable (e.g. function argument) should be done by using the strict equality operator.

  > Explanation:
  > - In modern browsers (`IE9+`, `Opera 12.16+`, `Firefox 4+`) [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined) is immutable (a non-configurable, non-writable property of the global object).
  > - It prevents undeclared variables usage.

  ```js
  // Bad
  typeof x === 'undefined';
  x === void 0;

  // Good
  x === undefined;
  ```

  **Exceptions:**

- `typeof` should be used if you need to support old browsers (like `IE8`) where `window.undefined` property is mutable.
- `typeof` may be used in place where `string` type is expected.

    ```js
    switch (typeof x) {
      case 'number':
        // ...
      case 'undefined':
        // ...
    }
    ```

- Checking for existence of a global variable should be done by using `typeof` operator or by checking existence of a property of the global object.

  > Explanation:
  > - An attempt to access undeclared variable will result in an error.

  ```js
  if (typeof Foo !== 'undefined') {
    // ...
  }

  // Also okay for browser only code (`window` is unavailable in Node.js)
  if (window.Foo !== undefined) {
    // ...
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Parentheses

- Should not be used with the unary operators `delete`, `typeof` and `void`, or with the keywords `return`, `throw` and `new`.

  ```js
  // Bad
  delete(obj.key);
  typeof(x) === 'number';
  new(Type)();
  throw(new Error());

  // Good
  delete obj.key;
  typeof x === 'number';
  new Type();
  throw new Error();
  ```

- Explicit parentheses in logical or mathematical expressions can be used to increase readability.

  ```js
  // equivalent to a - b > c && c || c + d && d + 1 || e
  ((a - b > c) && c) || (c + d && d + 1) || e;
  ```

**[⬆ back to TOC](#table-of-contents)**

## Exceptions

`throw` should be used with `new Error` or an object of a class derived from `Error`.

  ```js
  // Bad
  throw 'Plain message';

  // Good
  throw new Error('Error message');
  ```

**[⬆ back to TOC](#table-of-contents)**

## Type Casting

- Type casting should be done explicitly.
  * Strings: use the `String` global object directly;
  * Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings;
  * Booleans: use `Boolean` object constructor directly or `!!`.

  ```js
  // Bad
  new Boolean(foo);
  +bar;
  baz + '';
  ~[].indexOf(qux);
  var val = parseInt(inputVal);

  // Good
  Boolean(foo);
  !!foo;
  Number(bar);
  String(baz);
  [].indexOf(qux) === -1 or [].indexOf(qux) < 0;
  var val = parseInt(inputVal, 10);
  ```

**[⬆ back to TOC](#table-of-contents)**

## Multi-Line Statements

- If a statement is longer than the [maximum line length](#general-formatting), it's recommended to split it into several lines and properly indent.
- Lines of the statement should be split after an operator.

  ```js
  var debt = this.calculateBaseDebt() + this.calculateSharedDebt() + this.calculateDebtPayments() +
    this.calculateDebtFine();
  ```

- Closing parentheses should be on a new line with the indentation of the current block statement.

  ```js
  // Bad
  DoSomethingThatRequiresALongFunctionName(
    veryLongArgument1,
    argument2,
    argument3,
    argument4);
  anotherStatement;

  // Good
  DoSomethingThatRequiresALongFunctionName(
    veryLongArgument1,
    argument2,
    argument3,
    argument4
  );
  anotherStatement;
  ```

**[⬆ back to TOC](#table-of-contents)**

## Method Chaining

- When a method is called on a new line, it should:
  * be one indentation level deeper than the target object;
  * begin with the property access operator `.`

  ```js
  // Bad
  someObject.
   start().
   end();

  someObject
  .start()
  .end();

  // Good
  someObject
    .operation()
    .operationWithCallback(function (obj) {
      obj.processed = true;
    })
   .end();
  ```

**[⬆ back to TOC](#table-of-contents)**

## String Concatenation

- Strings should be concatenated with the `+` (string concatenation) operator.
- The `[].join('')` should be avoided.
- Escaping newline literals inside strings should be avoided.
- Each new line should be indented with 2 space characters.

  ```js
  // Bad
  var foo = 'A rather long string of English text, an error message \
            actually that just keeps going and going -- an error \
            message to make the Energizer bunny blush (right through \
            those Schwarzenegger shades)! Where was I? Oh yes, \
            you\'ve got an error and all the extraneous whitespace is \
            just gravy. Have a nice day.';

  // Good
  var foo = 'A rather long string of English text, an error message ' +
    'actually that just keeps going and going -- an error ' +
    'message to make the Energizer bunny blush (right through ' +
    'those Schwarzenegger shades)! Where was I? Oh yes, ' +
    'you\'ve got an error and all the extraneous whitespace is ' +
    'just gravy. Have a nice day.';
  ```

**[⬆ back to TOC](#table-of-contents)**

## Empty Lines

A single empty line can be used as a separator for grouping the code into logical blocks.

```js
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);
```

**[⬆ back to TOC](#table-of-contents)**

## Function Context

- Binding the context variable for function calls should be done using [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

  ```js
  doAsync(function () {
    this.fn();
  }.bind(this));
  ```

- Preferably, the context argument should be used (if available).

  ```js
  // Bad
  [1, 2, 3].forEach(function (n) {
    this.fn(n);
  }.bind(this));

  // Good
  [1, 2, 3].forEach(function (n) {
    this.fn(n);
  }, this);
  ```

- If assigning the current context to a variable, the variable should be named `_this`.

  ```js
  // Bad
  var that = this;
  vat self = this;

  // Good
  var _this = this;
  doAsync(function () {
    _this.fn();
  });
  ```

**[⬆ back to TOC](#table-of-contents)**

## Comments

- In-line (single-line) comments should start with `//`. Between the `//` and the text of the comment should be 1 space character. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.
- Always begin sentences with an upper case.
- No trailing `.` unless comment contains multiple sentences.
- Formal style, consistent voice, no humor, present tense.
- No developer name or other personal notes.
- Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.
- Comments for functions, methods, classes, etc. should be written according to the [JSDoc](http://usejsdoc.org/) documentation syntax, using `/** ... */`.

  ```js
  // Bad

  // Return a new element
  // based on the passed in tag name
  function make(tag) {
    console.log('fetching type...');
    // set the default type to 'no type'
    var type = this._type || 'no type';

    var active = true;  // is current element

    // ...

    return element;
  }

  // Good

  /**
   * Return a new element based on the passed in tag name.
   *
   * @param {string} tag Tag name
   * @returns {Element} element
   */
  function make(tag) {
    console.log('fetching type...');

    // Set the default type to 'no type'
    var type = this._type || 'no type';

    // Is current tab
    const active = true;

    // ...

    return element;
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Classes

- "Symmetrical" methods should be declared one after the other.

  ```js
  var SampleClass = inherit({
    __constructor: function () {},

    // Destructors are placed right after the constructor
    destruct: function () {},

    someMethod: function () {}
  });
  ```
- Methods can return `this` to help with method chaining.

  ```js
  class Jedi {
    jump() {
      this.jumping = true;
      return this;
    }

    setHeight(height) {
      this.height = height;
      return this;
    }
  }

  const luke = new Jedi();

  luke
    .jump()
    .setHeight(20);
  ```

- Prefix private prototype members with `_`.

  ```js
  Example.prototype.method = function () {
    this.public = 'external';
    this._private = 'internal';
  }
  ```

- Enforce new on Constructor.

  Use `this instanceof` to check if a constructor function was called with new. (This allows for future prototypical inheritance)

  ```js
  if (this instanceof ConstructorName) {
    // ...
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Enums

- Enum names should be in `UpperCamelCase`.
- Enum members should be in `ALL_CAPS`.

```js
var Color = {
  BLUE: '#00d',
  RED: '#d00'
};
```

**[⬆ back to TOC](#table-of-contents)**

## Events

- When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

  ```js
  // Bad
  $(this).trigger('itemUpdated', item.id);

  $(this).on('itemUpdated', (e, itemId) => {
    // Do something with itemId
  });
  ```

  prefer:

  ```js
  // Good
  $(this).trigger('itemUpdated', { itemId: item.id });

  $(this).on('itemUpdated', (e, data) => {
    // Do something with data.itemId
  });
  ```

**[⬆ back to TOC](#table-of-contents)**

## jQuery

- Prefix jQuery object variables with a `$`.

  ```js
  // Bad
  var target = $('.target');

  // Good
  var $target = $('.target');
  ```

- Cache jQuery lookups.
- Use `find` method with scoped jQuery object queries.

  ```js
  // Bad
  $('nav').find('ul').hide();

  // Good
  $target.find('ul').hide();
  ```

**[⬆ back to TOC](#table-of-contents)**

## Testing

- **Yup.**
- Whichever [testing framework](https://coderwall.com/p/ntbixw/javascript-test-framework-comparison) you use, you should be writing tests!
- Strive to write many small pure functions, and minimize where mutations occur.
- 100% test coverage is a good goal to strive for, even if it's not always practical to reach it.

**[⬆ back to top](#table-of-contents)**

## Performance

- [On Layout & Web Performance](http://www.kellegous.com/j/2013/01/26/layout-performance/)
- [String vs Array Concat](http://jsperf.com/string-vs-array-concat/18)
- [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost/10)
- [Bang Function](http://jsperf.com/bang-function/48)
- [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/153)
- [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text/18)
- [Long String Concatenation](http://jsperf.com/ya-string-concat/35)

**[⬆ back to top](#table-of-contents)**

## Resources

**Other Style Guides**

  - [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
  - [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
  - [GitHub JavaScript styleguide](https://github.com/styleguide/javascript)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [jQuery JavaScript Style Guide](http://contribute.jquery.org/style-guide/js/)

**Other Styles**

  - [Ideas on naming this in nested functions](https://gist.github.com/cjohansen/4135065)
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52)
  - [Popular JavaScript Coding Conventions on Github](http://sideeffect.kr/popularconvention/#javascript)
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/)

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**[⬆ back to top](#table-of-contents)**
