---
id: babel-plugin-transform-named-capturing-groups-regex
title: "@babel/plugin-transform-named-capturing-groups-regex"
sidebar_label: named-capturing-groups-regex
---

:::info
This plugin is included in `@babel/preset-env`, in [ES2018](https://github.com/tc39/proposals/blob/master/finished-proposals.md)
NOTE: This plugin generates code that needs ES6 regular expressions
functionalities. If you need to support older browsers, use either
the `runtime: false` option or import a proper polyfill (e.g. `core-js`).
:::

This plugin transforms regular expression _literals_ to support named capturing groups. It does not patch the `new RegExp` constructor, since its arguments cannot be pre-transformed statically: to handle runtime behavior of functions/classes, you will need to use a polyfill instead.

## Examples

**In**

```js title="JavaScript"
var re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

console.log(re.exec("1999-02-29").groups.year);
```

**Out**

```js title="JavaScript"
var re = _wrapRegExp(/(\d{4})-(\d{2})-(\d{2})/, { year: 1, month: 2, day: 3 });

console.log(re.exec("1999-02-29").groups.year);
```

## Installation

```shell npm2yarn
npm install --save-dev @babel/plugin-transform-named-capturing-groups-regex
```

## Usage

### With a configuration file (Recommended)

```json title="babel.config.json"
{
  "plugins": ["@babel/plugin-transform-named-capturing-groups-regex"]
}
```

### Via CLI

```sh title="Shell"
babel --plugins @babel/plugin-transform-named-capturing-groups-regex script.js
```

### Via Node API

```js title="JavaScript"
require("@babel/core").transformSync("code", {
  plugins: ["@babel/plugin-transform-named-capturing-groups-regex"],
});
```

## Options

### `runtime`

`boolean`, defaults to `true`

When this option is disabled, Babel doesn't wrap RegExps with the `_wrapRegExp` helper.
The output only supports internal group references, and not runtime properties:

```js title="JavaScript"
var stringRe = /(?<quote>"|').*?\k<quote>/;

stringRe.test("'foo'"); // "true", works
stringRe.exec("'foo'").groups.quote; // Error
```

:::tip
You can read more about configuring plugin options [here](https://babeljs.io/docs/en/plugins#plugin-options)
:::
