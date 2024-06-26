---
id: babel-plugin-transform-dotall-regex
title: "@babel/plugin-transform-dotall-regex"
sidebar_label: dotall-regex
---

:::info
This plugin is included in `@babel/preset-env`, in [ES2018](https://github.com/tc39/proposals/blob/master/finished-proposals.md)
:::

This plugin transforms regular expression _literals_ to support the `/s` flag. It does not patch the `new RegExp` constructor, since its arguments cannot be pre-transformed statically: to handle runtime behavior of functions/classes, you will need to use a polyfill instead.

## Example

**In**

```js title="JavaScript"
/./s;
```

**Out**

```js title="JavaScript"
/[\0-\uFFFF]/;
```

**In**

```js title="JavaScript"
/./su;
```

**Out**

```js title="JavaScript"
/[\0-\u{10FFFF}]/u;
```

[Here’s an online demo.](https://mothereff.in/regexpu#input=const+regex+%3D+/foo.bar/s%3B%0Aconsole.log%28%0A++regex.test%28%27foo%5Cnbar%27%29%0A%29%3B%0A//+%E2%86%92+true&dotAllFlag=1)

## Installation

```shell npm2yarn
npm install --save-dev @babel/plugin-transform-dotall-regex
```

## Usage

### With a configuration file (Recommended)

`.babelrc`

```json title="babel.config.json"
{
  "plugins": ["@babel/plugin-transform-dotall-regex"]
}
```

### Via CLI

```sh title="Shell"
$ babel --plugins @babel/plugin-transform-dotall-regex script.js
```

### Via Node.js API

```js title="JavaScript"
require("@babel/core").transformSync(code, {
  plugins: ["@babel/plugin-transform-dotall-regex"],
});
```

## Author

| [![twitter/mathias](https://gravatar.com/avatar/24e08a9ea84deb17ae121074d0f17125?s=70)](https://twitter.com/mathias "Follow @mathias on Twitter") |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Mathias Bynens](https://mathiasbynens.be/)                                                                                                       |
