# ESLint Config Pack

## Installation

Install [ESLint](https://www.github.com/eslint/eslint) either locally or globally.

```sh
$ npm install --save-dev eslint
```

## For ECMAScript 5

Append content of [`es5.js`](es5.js) in your [`.eslintrc.js`](../.eslintrc.js) file.

## For ECMAScript 6

Append content of [`es6.js`](es6.js) in your [`.eslintrc.js`](../.eslintrc.js) file.

## For React

- Install React plugin for `ESLint`. If you installed `ESLint` globally, you have to install React plugin globally too. Otherwise, install it locally.

  ```sh
  $ npm install --save-dev eslint-plugin-react
  ```

- Inject React specific [linting rules](react.js) for ESLint [config file](../.eslintrc.js).
- Adjust `extends` section of the [config file](../.eslintrc.js), so it reads like that:

  ```json
  "extends": ["eslint:recommended", "plugin:react/recommended"]
  ```

## For Node.js

Append content of [`node.js`](node.js) into your [`.eslintrc.js`](../.eslintrc.js) file.
