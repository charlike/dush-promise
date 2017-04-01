# dush-promise [![npm version][npmv-img]][npmv-url] [![github tags][ghtag-img]][ghtag-url] [![mit license][license-img]][license-url]

> Plugin for `dush` that makes it a Deferred promise and adds `.resolve`, `.reject`, `.than` and `.catch` methods for more better error handling experience

You might also be interested in [dush](https://github.com/tunnckocore/dush#readme).

## Quality 👌

> By using [commitizen][czfriendly-url] and [conventional commit messages][conventional-messages-url], 
maintaining meaningful [ChangeLog][changelogmd-url] 
and commit history based on [global conventions][conventions-url], 
following [StandardJS][standard-url] code style through [ESLint][eslint-url] and
having always up-to-date dependencies through integrations
like [GreenKeeper][gk-integration-url] and [David-DM][daviddm-url] service,
this package has top quality.

[![code climate][codeclimate-img]][codeclimate-url] 
[![code style][standard-img]][standard-url] 
[![commitizen friendly][czfriendly-img]][czfriendly-url] 
[![greenkeeper friendly][gkfriendly-img]][gkfriendly-url] 
[![dependencies][daviddm-deps-img]][daviddm-deps-url] 
<!-- uncomment when need -->
<!-- [![develop deps][daviddm-devdeps-img]][daviddm-devdeps-url] -->

## Stability 💯

> By following [Semantic Versioning][semver-url] through [standard-version][] releasing tool, 
this package is very stable and its tests are passing both on [Windows (AppVeyor)][appveyor-ci-url] 
and [Linux (CircleCI)][circle-ci-url] with results 
from 100% to [400%][absolute-coverage-url] test coverage, reported respectively
by [CodeCov][codecov-coverage-url] and [nyc (istanbul)][nyc-istanbul-url].

[![following semver][following-semver-img]][following-semver-url] 
[![semantic releases][strelease-img]][strelease-url] 
[![linux build][circle-img]][circle-url] 
[![windows build][appveyor-img]][appveyor-url] 
[![code coverage][codecov-img]][codecov-url] 
[![nyc coverage][istanbulcov-img]][istanbulcov-url] 

## Support :clap:

> If you have any problems, consider opening [an issue][open-issue-url],
ping me on twitter ([@tunnckoCore][tunnckocore-twitter-url]),
join the [support chat][supportchat-url] room
or queue a [live session][codementor-url] on CodeMentor with me.
If you don't have any problems, you're using it somewhere or
you just enjoy this product, then please consider [donating some cash][paypalme-url] at PayPal,
since this is [OPEN Open Source][opensource-project-url] project made
with love at [Sofia, Bulgaria][bulgaria-url] 🇧🇬.

[![tunnckoCore support][supportchat-img]][supportchat-url] 
[![code mentor][codementor-img]][codementor-url] 
[![paypal donate][paypalme-img]][paypalme-url] 
[![NPM monthly downloads](https://img.shields.io/npm/dm/dush-promise.svg?style=flat)](https://npmjs.org/package/dush-promise) 
[![npm total downloads][downloads-img]][downloads-url] 

## Table of Contents
- [Install](#install)
- [Usage](#usage)
- [API](#api)
  * [dushPromise](#dushpromise)
  * [.then](#then)
  * [.catch](#catch)
  * [.resolve](#resolve)
  * [.reject](#reject)
- [Related](#related)
- [Contributing](#contributing)
- [Building docs](#building-docs)
- [Running tests](#running-tests)
- [Author](#author)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install
Install with [npm](https://www.npmjs.com/)

```
$ npm install dush-promise --save
```

or install using [yarn](https://yarnpkg.com)

```
$ yarn add dush-promise
```

## Usage
> For more use-cases see the [tests](test.js)

```js
const dushPromise = require('dush-promise')
```

## API

### [dushPromise](index.js#L38)
> Adds a Promise methods such as `.resolve`, `.reject` `.then` and `.catch` to your [dush][] application. Useful from inside plugins. This plugin also emits `error` event when `app.reject` is used.

**Params**

* `opts` **{Object}**: optional, passed directly to [native-promise-deferred][]    
* `returns` **{Function}**: a plugin function that should be passed to `.use` method of [dush][]  

**Example**

```js
var dush = require('dush')
var promise = require('dush-promise')

var app = dush().use(promise())

console.log(app.then)
console.log(app.catch)
console.log(app.reject)
console.log(app.resolve)
```

### [.then](index.js#L68)
> Handle resolved promise with `onresolved` or rejected promise with `onrejected`. It is as any usual Promise `.then` method.

**Params**

* `onresolved` **{Function}**    
* `onrejected` **{Function}**    
* `returns` **{Promise}**  

**Example**

```js
app.then((res) => {
  console.log(res) // => 123
})
app.resolve(123)

// or handle rejected promise
app.then(null, (er) => {
  console.log('err!', er) // => Error: foo bar
})
app.reject(new Error('foo bar'))
```

### [.catch](index.js#L95)
> Catch a rejected promise error. This method is mirror of any usual promise `.catch` method.

**Params**

* `onrejected` **{Function}**    
* `returns` **{Promise}**  

**Example**

```js
app.on('error', (err) => {
  console.log('er!', err) // => Error: sad err
})
app.catch((err) => {
  console.log('oops, error!', err) // => Error: sad err
})

app.reject(new Error('sad err'))
```

### [.resolve](index.js#L123)
> As any usual `Promise.resolve` method.

**Params**

* `val` **{any}**    
* `returns` **{Promise}**  

**Example**

```js
app.use((app) => {
  app.foo = () => {
    return app.resolve(1222)
  }
})

const promise = app.foo()
promise.then((val) => {
  console.log('res:', val) // => 1222
})
```

### [.reject](index.js#L145)
> As any usual `Promise.reject` method.

**Params**

* `err` **{Error}**    
* `returns` **{Promise}**  

**Example**

```js
app.on('error', (err) => {
  console.log('some error:', err) // => Error: quxie
})
app.reject(new Error('quxie'))
```

## Related
- [dush-methods](https://www.npmjs.com/package/dush-methods): Plugin for `dush` and anything based on it. It adds helper `.define` and `.delegate` methods | [homepage](https://github.com/tunnckocore/dush-methods#readme "Plugin for `dush` and anything based on it. It adds helper `.define` and `.delegate` methods")
- [dush-no-chaining](https://www.npmjs.com/package/dush-no-chaining): A plugin that removes the emitter methods chaining support for `dush`, `base`, `minibase` or anything based on them | [homepage](https://github.com/tunnckocore/dush-no-chaining#readme "A plugin that removes the emitter methods chaining support for `dush`, `base`, `minibase` or anything based on them")
- [dush-options](https://www.npmjs.com/package/dush-options): Adds `.option`, `.enable` and `.disable` methods to your `dush` application | [homepage](https://github.com/tunnckocore/dush-options#readme "Adds `.option`, `.enable` and `.disable` methods to your `dush` application")
- [dush-router](https://www.npmjs.com/package/dush-router): A simple regex-based router for `dush`, `base`, `minibase` and anything based on them. Works on Browser and Node.js | [homepage](https://github.com/tunnckocore/dush-router#readme "A simple regex-based router for `dush`, `base`, `minibase` and anything based on them. Works on Browser and Node.js")
- [dush-tap-report](https://www.npmjs.com/package/dush-tap-report): A simple TAP report producer based on event system. A plugin for `dush` event emitter or anything based on it | [homepage](https://github.com/tunnckocore/dush-tap-report#readme "A simple TAP report producer based on event system. A plugin for `dush` event emitter or anything based on it")
- [dush](https://www.npmjs.com/package/dush): Microscopic & functional event emitter in ~260 bytes, extensible through plugins. | [homepage](https://github.com/tunnckocore/dush#readme "Microscopic & functional event emitter in ~260 bytes, extensible through plugins.")
- [minibase-create-plugin](https://www.npmjs.com/package/minibase-create-plugin): Utility for [minibase][] and [base][] that helps you create plugins | [homepage](https://github.com/node-minibase/minibase-create-plugin#readme "Utility for [minibase][] and [base][] that helps you create plugins")
- [minibase](https://www.npmjs.com/package/minibase): Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing… [more](https://github.com/node-minibase/minibase#readme) | [homepage](https://github.com/node-minibase/minibase#readme "Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing [base][] plugins.")
- [native-or-another](https://www.npmjs.com/package/native-or-another): Guaranteed way for getting a Promise. Always native Promise if available, otherwise looks for common promise libraries and loads which… [more](https://github.com/tunnckocore/native-or-another#readme) | [homepage](https://github.com/tunnckocore/native-or-another#readme "Guaranteed way for getting a Promise. Always native Promise if available, otherwise looks for common promise libraries and loads which is installed. Allows registering custom Promise implementation in node < 0.12 versions")
- [native-promise-deferred](https://www.npmjs.com/package/native-promise-deferred): A deferred Promise, using `native-or-another` behind and so it work on Node.js v0.10 too! | [homepage](https://github.com/tunnckocore/native-promise-deferred#readme "A deferred Promise, using `native-or-another` behind and so it work on Node.js v0.10 too!")
- [native-promise](https://www.npmjs.com/package/native-promise): Get native `Promise` or falsey value if not available. | [homepage](https://github.com/tunnckocore/native-promise#readme "Get native `Promise` or falsey value if not available.")

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue][open-issue-url].  
Please read the [contributing guidelines][contributing-url] for advice on opening issues, pull requests, and coding standards.  
If you need some help and can spent some cash, feel free to [contact me at CodeMentor.io][codementor-url] too.

**In short:** If you want to contribute to that project, please follow these things

1. Please DO NOT edit [README.md](README.md), [CHANGELOG.md][changelogmd-url] and [.verb.md](.verb.md) files. See ["Building docs"](#building-docs) section.
2. Ensure anything is okey by installing the dependencies and run the tests. See ["Running tests"](#running-tests) section.
3. Always use `npm run commit` to commit changes instead of `git commit`, because it is interactive and user-friendly. It uses [commitizen][] behind the scenes, which follows Conventional Changelog idealogy.
4. Do NOT bump the version in package.json. For that we use `npm run release`, which is [standard-version][] and follows Conventional Changelog idealogy.

Thanks a lot! :)

## Building docs
Documentation and that readme is generated using [verb-generate-readme][], which is a [verb][] generator, so you need to install both of them and then run `verb` command like that

```
$ npm install verbose/verb#dev verb-generate-readme --global && verb
```

_Please don't edit the README directly. Any changes to the readme must be made in [.verb.md](.verb.md)._

## Running tests
Clone repository and run the following in that cloned directory

```
$ npm install && npm test
```

## Author
**Charlike Mike Reagent**

+ [github/tunnckoCore](https://github.com/tunnckoCore)
+ [twitter/tunnckoCore](https://twitter.com/tunnckoCore)
+ [codementor/tunnckoCore](https://codementor.io/tunnckoCore)

## License
Copyright © 2017, [Charlike Mike Reagent](https://i.am.charlike.online). Released under the [MIT License](LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.4.3, on April 01, 2017._  
_Project scaffolded using [charlike][] cli._

[always-done]: https://github.com/hybridables/always-done
[async-done]: https://github.com/gulpjs/async-done
[base]: https://github.com/node-base/base
[charlike]: https://github.com/tunnckocore/charlike
[commitizen]: https://github.com/commitizen/cz-cli
[dezalgo]: https://github.com/npm/dezalgo
[dush]: https://github.com/tunnckocore/dush
[native-promise-deferred]: https://github.com/tunnckocore/native-promise-deferred
[once]: https://github.com/isaacs/once
[standard-version]: https://github.com/conventional-changelog/standard-version
[type]: https://github.com/Gozala/type
[verb-generate-readme]: https://github.com/verbose/verb-generate-readme
[verb]: https://github.com/verbose/verb

[license-url]: https://github.com/tunnckoCore/dush-promise/blob/master/LICENSE
[license-img]: https://img.shields.io/npm/l/dush-promise.svg

[downloads-url]: https://www.npmjs.com/package/dush-promise
[downloads-img]: https://img.shields.io/npm/dt/dush-promise.svg

[codeclimate-url]: https://codeclimate.com/github/tunnckoCore/dush-promise
[codeclimate-img]: https://img.shields.io/codeclimate/github/tunnckoCore/dush-promise.svg

[circle-url]: https://circleci.com/gh/tunnckoCore/dush-promise
[circle-img]: https://img.shields.io/circleci/project/github/tunnckoCore/dush-promise/master.svg?label=linux

[appveyor-url]: https://ci.appveyor.com/project/tunnckoCore/dush-promise
[appveyor-img]: https://img.shields.io/appveyor/ci/tunnckoCore/dush-promise/master.svg?label=windows

[codecov-url]: https://codecov.io/gh/tunnckoCore/dush-promise
[codecov-img]: https://img.shields.io/codecov/c/github/tunnckoCore/dush-promise/master.svg?label=codecov

[daviddm-deps-url]: https://david-dm.org/tunnckoCore/dush-promise
[daviddm-deps-img]: https://img.shields.io/david/tunnckoCore/dush-promise.svg

[daviddm-devdeps-url]: https://david-dm.org/tunnckoCore/dush-promise?type=dev
[daviddm-devdeps-img]: https://img.shields.io/david/dev/tunnckoCore/dush-promise.svg

[ghtag-url]: https://github.com/tunnckoCore/dush-promise/releases/tag/v1.0.1
[ghtag-img]: https://img.shields.io/github/tag/tunnckoCore/dush-promise.svg?label=github%20tag

[npmv-url]: https://www.npmjs.com/package/dush-promise
[npmv-img]: https://img.shields.io/npm/v/dush-promise.svg?label=npm%20version

[standard-url]: https://github.com/feross/standard
[standard-img]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg

[paypalme-url]: https://www.paypal.me/tunnckoCore
[paypalme-img]: https://img.shields.io/badge/paypal-donate-brightgreen.svg

[czfriendly-url]: http://commitizen.github.io/cz-cli
[czfriendly-img]: https://img.shields.io/badge/commitizen-friendly-brightgreen.svg

[gkfriendly-url]: https://greenkeeper.io/
[gkfriendly-img]: https://img.shields.io/badge/greenkeeper-friendly-brightgreen.svg

[codementor-url]: https://www.codementor.io/tunnckocore?utm_source=github&utm_medium=button&utm_term=tunnckocore&utm_campaign=github
[codementor-img]: https://img.shields.io/badge/code%20mentor-live%20session-brightgreen.svg

[istanbulcov-url]: https://twitter.com/tunnckoCore/status/841768516965568512
[istanbulcov-img]: https://img.shields.io/badge/istanbul-400%25-brightgreen.svg

[following-semver-url]: http://semver.org
[following-semver-img]: https://img.shields.io/badge/following-semver-brightgreen.svg

[strelease-url]: https://github.com/conventional-changelog/standard-version
[strelease-img]: https://img.shields.io/badge/using-standard%20version-brightgreen.svg

[supportchat-url]: https://gitter.im/tunnckoCore/support
[supportchat-img]: https://img.shields.io/gitter/room/tunnckoCore/support.svg

[bulgaria-url]: https://www.google.bg/search?q=Sofia%2C+Bulgaria "One of the top 10 best places for start-up business in the world, especially in IT technologies"

[changelogmd-url]: https://github.com/tunnckoCore/dush-promise/blob/master/CHANGELOG.md
[conventions-url]: https://github.com/bcoe/conventional-changelog-standard/blob/master/convention.md
[tunnckocore-twitter-url]: https://twitter.com/tunnckoCore
[opensource-project-url]: http://openopensource.org
[nyc-istanbul-url]: https://istanbul.js.org
[circle-ci-url]: https://circleci.com
[appveyor-ci-url]: https://appveyor.com
[codecov-coverage-url]: https://codecov.io
[semver-url]: http://semver.org
[eslint-url]: http://eslint.org
[conventional-messages-url]: https://github.com/conventional-changelog/conventional-changelog
[gk-integration-url]: https://github.com/integration/greenkeeper
[daviddm-url]: https://david-dm.org
[open-issue-url]: https://github.com/tunnckoCore/dush-promise/issues/new
[contributing-url]: https://github.com/tunnckoCore/dush-promise/blob/master/CONTRIBUTING.md
[absolute-coverage-url]: https://github.com/tunnckoCore/dush-promise/blob/master/package.json

[minibase]: https://github.com/node-minibase/minibase