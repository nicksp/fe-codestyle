# Node.js Style Guide

This section outlines styling rules for [Node.js](https://nodejs.org/dist/latest-v5.x/docs/api/all.html) code. It's inspired by what is popular within the community, and flavored with some personal opinions.

## Table of Contents

  1. [Formatting](#formatting)
  1. [Naming Conventions](#naming-conventions)
  1. [Importing Modules](#importing-modules)
  1. [Module Globals](#module-globals)
  1. [Callbacks](#callbacks)
  1. [Promises](#promises)
  1. [Miscellaneous](#miscellaneous)

## Formatting

- Files should be encoded in **UTF-8** without BOM.
- Use 2 spaces for indenting your code. Never mix tabs and spaces.
- Use UNIX-style newlines `LF` (`\n`), and a newline character as the last character of a file.
- Clean up any trailing whitespace in your JS files before committing.
- Try to be explicit: **use semicolons**.
- Limit your lines to 120 characters.
- Use single quotes for strings, unless you are writing JSON.

  ```js
  // Bad
  let foo = "foo";

  // Good
  let foo = 'foo';
  ```

- Opening braces go on the same line as the statement.

  ```js
  // Bad
  if (true)
  {
    console.log('bad style');
  }

  // Good
  if (true) {
    console.log('correct style');
  }
  ```

- For **var declarations**, write each declaration in its own statement on its own line. And put the declarations wherever they make sense.

  ```js
  // Bad
  let silent = true, verbose = true;

  let silent = true,
      verbose = true;

  let keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

  while (keys.length) {
    key = keys.pop();
    object[key] = values.pop();
  }

  // Good
  let silent = true;
  let verbose = true;

  let keys   = ['foo', 'bar'];
  let values = [23, 42];

  let object = {};
  while (keys.length) {
    let key = keys.pop();
    object[key] = values.pop();
  }
  ```

- Wrap conditional assignments with additional parentheses. This makes it clear that the expression is intentionally an assignment (`=`) rather than a typo for equality (`===`).

  ```js
  // Bad
  while (eq = text.match(expr)) {
    // code
  }

  // Good
  while ((eq = text.match(expr))) {
    // code
  }
  ```

**[⬆ back to TOC](#table-of-contents)**

## Naming Conventions

- Use **lowerCamelCase** for variables, properties and function/method names.

  ```js
  // Bad
  let var_name = 'local variable';

  // Good
  let varName = 'local variable';
  ```

- Use **UpperCamelCase** for class names.

  ```js
  // Bad
  function person_information() {
    // code
  }

  // Good
  function PersonInformation() = {
    // code
  }
  ```

- Use **UPPERCASE** for constants.

  ```js
  const PI = 3.14159265359;
  Utils.MAGIC_NUM = 777;
  ```

**[⬆ back to TOC](#table-of-contents)**

## Importing Modules

- Modules should be imported in the beginning of the file (*to clearly illustrate a file's dependencies*), after the description of the module (if present):

  ```js
  // Bad
  let http = require('http');

  // code here

  let fs = require('fs');

  // code here

  // Good
  let http = require('http');
  let fs = require('fs');

  // code here
  ```

  **Exception:** This rule does not apply to modules that are imported "on demand", inside `if` condition for example.

- Always use relative paths.

- Module import calls should be grouped according to the following order:

  1. Standard node.js modules (i.e. fs, util, etc.)
  2. External lib modules
  3. Modules of the current application

**[⬆ back to TOC](#table-of-contents)**

## Module Globals

- Every module can only have two top level globals (except for imported modules):
  * `exports` - defined automatically by node
  * `internals` - must be declared as an object at the top of each module immediate following the `require` section.
- Any variable global to the module must be a property of `internals`, including constants.
- If a module has automatically executing code, it must be contained within a function (using the `internals` namespace) and called at the top of the module after the `internals` declaration.

  ```js
  // Bad
  const foo = 'bar'; // No global vars outside of internals

  const internals = {
    Foo: 'bar' // Don't use uppercase vars inside internals
  };

  const server = new Hapi.Server(); // No global vars outside of internals and exports / Set up your module inside an init() function

  <...>

  const Module = require('module'); // Require modules at the top of the module

  // Good

  // Load modules
  const Server = require('server');
  const Items = require('items');
  const Methods = require('./methods');

  // Declare internals
  const internals = {};

  internals.package = require('./package.json');
  internals.foo = 'bar';

  internals.init = function () {
    const server = new Server();
    // code here
  };

  internals.init();
  ```

**[⬆ back to TOC](#table-of-contents)**

## Callbacks

- First argument must always be `err`.
- Inline callbacks must use arrow functions.
- If a function takes a `callback` argument, it must be called on `process.nextTick()`. Otherwise, the argument name **must** be `next` to clearly declare that it may get called on same tick.
- Callbacks should always be called with explicit `return`.

**[⬆ back to TOC](#table-of-contents)**

## Promises

- Public interfaces should return a promise when no callback is provided.
- Promises should not be used internally.
- Only native promises are allowed. Third party promise implementations are not allowed.

**[⬆ back to TOC](#table-of-contents)**

## Miscellaneous

- `err` is reserved for errors received via a callback. Use `error` for local function variables.
- Stay away from using **Object.freeze, Object.preventExtensions, Object.seal, with, eval**.

**[⬆ back to TOC](#table-of-contents)**
