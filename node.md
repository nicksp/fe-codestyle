# Node.js Style Guide

This section outlines styling rules for [Node.js](https://nodejs.org/dist/latest-v5.x/docs/api/all.html) code.

## Table of Contents

  1. [Importing Modules](#importing-modules)

## Importing Modules

- Modules should be imported in the beginning of the file, after the description of the module (if present):

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

- Module import calls should be grouped according to the following order:

  1. Standard node.js modules (i.e. fs, util, etc.)
  2. External lib modules
  3. Modules of the current application

**[⬆ back to TOC](#table-of-contents)**
