# ESLint Config Pack

## Installation

Install [ESLint](https://www.github.com/eslint/eslint) either locally or globally.

```sh
$ npm install --save-dev eslint
```

## For ECMAScript 5

Append content of [`es5.js`](es5.js) in your [`.eslintrc`](../.eslintrc) file.

## For ECMAScript 6

Append content of [`es6.js`](es6.js) in your [`.eslintrc`](../.eslintrc) file.

## For React

- Install React plugin for `ESLint`. If you installed `ESLint` globally, you have to install React plugin globally too. Otherwise, install it locally.

  ```sh
  $ npm install --save-dev eslint-plugin-react
  ```

- Inject React specific [linting rules](react.js) for ESLint [config file](../.eslintrc).

## For Node.js

Append content of [`node.js`](node.js) in your [`.eslintrc`](../.eslintrc) file.
