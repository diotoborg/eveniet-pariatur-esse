# @diotoborg/eveniet-pariatur-esse <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

> Returns true if a value has the characteristics of a valid JavaScript descriptor. Works for fully completed data descriptors and accessor descriptors.

## Usage

```js
const isDescriptor = require('@diotoborg/eveniet-pariatur-esse');
const assert = require('assert');

const defaults = { configurable: false, enumerable: false };
const dataDefaults = { ...defaults, writable: false};

assert.ok(isDescriptor({ ...dataDefaults, value: 'foo' }));
assert.ok(isDescriptor({ ...defaults, get() {}, set() {} }));
assert.ok(!isDescriptor({ ...defaults, get: 'foo', set() {} }));
```

You may also check for a descriptor by passing an object as the first argument and property name (`string`) as the second argument.

```js
const obj = { foo: 'abc' };

Object.defineProperty(obj, 'bar', { value: 'xyz' });
Reflect.defineProperty(obj, 'baz', { value: 'xyz' });

assert.equal(isDescriptor(obj, 'foo'), true);
assert.equal(isDescriptor(obj, 'bar'), true);
assert.equal(isDescriptor(obj, 'baz'), true);
```

## Examples

### value type

Returns `false` when not an object

```js
assert.equal(isDescriptor('a'), false);
assert.equal(isDescriptor(null), false);
assert.equal(isDescriptor([]), false);
```

### data descriptor

Returns `true` when the object has valid properties with valid values.

```js
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo' }), true);
assert.equal(isDescriptor({ ...dataDefaults, value() {} }), true);
```

Returns `false` when the object has invalid properties

```js
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', bar: 'baz' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', bar: 'baz' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', enumerable: 'baz' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', configurable: 'baz' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', get() {} }), false);
assert.equal(isDescriptor({ ...dataDefaults, get() {}, value() {} }), false);
```

`false` when a value is not the correct type

```js
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', enumerable: 'foo' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', configurable: 'foo' }), false);
assert.equal(isDescriptor({ ...dataDefaults, value: 'foo', writable: 'foo' }), false);
```

### accessor descriptor

`true` when the object has valid properties with valid values.

```js
assert.equal(isDescriptor({ ...defaults, get() {}, set() {} }), true);
assert.equal(isDescriptor({ ...defaults, get() {} }), true);
assert.equal(isDescriptor({ ...defaults, set() {} }), true);
```

`false` when the object has invalid properties

```js
assert.equal(isDescriptor({ ...defaults, get() {}, set() {}, bar: 'baz' }), false);
assert.equal(isDescriptor({ ...defaults, get() {}, set() {}, enumerable: 'baz' }), false);
assert.equal(isDescriptor({ ...defaults, get() {}, writable: true }), false);
assert.equal(isDescriptor({ ...defaults, get() {}, value: true }), false);
```

Returns `false` when an accessor is not a function

```js
assert.equal(isDescriptor({ ...defaults, get() {}, set: 'baz' }), false);
assert.equal(isDescriptor({ ...defaults, get: 'foo', set() {} }), false);
assert.equal(isDescriptor({ ...defaults, get: 'foo', bar: 'baz' }), false);
assert.equal(isDescriptor({ ...defaults, get: 'foo', set: 'baz' }), false);
```

Returns `false` when a value is not the correct type

```js
assert.equal(isDescriptor({ ...defaults, get() {}, set() {}, enumerable: 'foo' }), false);
assert.equal(isDescriptor({ ...defaults, set() {}, configurable: 'foo' }), false);
assert.equal(isDescriptor({ ...defaults, get() {}, configurable: 'foo' }), false);
```

### Related projects

You might also be interested in these projects:

* [is-accessor-descriptor](https://www.npmjs.com/package/is-accessor-descriptor): Returns true if a value has the characteristics of a valid JavaScript accessor descriptor.
* [is-data-descriptor](https://www.npmjs.com/package/is-data-descriptor): Returns true if a value has the characteristics of a valid JavaScript data descriptor.
* [is-object](https://www.npmjs.com/package/is-object): Returns true if the value is an object and not an array or null.

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@diotoborg/eveniet-pariatur-esse
[npm-version-svg]: https://versionbadg.es/inspect-js/@diotoborg/eveniet-pariatur-esse.svg
[deps-svg]: https://david-dm.org/inspect-js/@diotoborg/eveniet-pariatur-esse.svg
[deps-url]: https://david-dm.org/inspect-js/@diotoborg/eveniet-pariatur-esse
[dev-deps-svg]: https://david-dm.org/inspect-js/@diotoborg/eveniet-pariatur-esse/dev-status.svg
[dev-deps-url]: https://david-dm.org/inspect-js/@diotoborg/eveniet-pariatur-esse#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/eveniet-pariatur-esse.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/eveniet-pariatur-esse.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/eveniet-pariatur-esse.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/eveniet-pariatur-esse
[codecov-image]: https://codecov.io/gh/inspect-js/@diotoborg/eveniet-pariatur-esse/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/inspect-js/@diotoborg/eveniet-pariatur-esse/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/inspect-js/@diotoborg/eveniet-pariatur-esse
[actions-url]: https://github.com/diotoborg/eveniet-pariatur-esse/actions
