# puppeteer-extra

[![npm](https://img.shields.io/npm/v/puppeteer-extra.svg)](https://www.npmjs.com/package/puppeteer-extra) 
[![npm](https://img.shields.io/npm/dt/puppeteer-extra.svg)](https://www.npmjs.com/package/puppeteer-extra) 
[![npm](https://img.shields.io/npm/l/puppeteer-extra.svg)](https://www.npmjs.com/package/puppeteer-extra)

[![extra](https://i.imgur.com/2ZjXBe5.jpg)](https://github.com/berstend/puppeteer-extra)

> A light-weight wrapper around [`puppeteer`](https://github.com/GoogleChrome/puppeteer) to enable [plugins](#plugins) through a clean interface.


## Installation

```bash
yarn add puppeteer puppeteer-extra

# or to install the latest tip-of-tree version of puppeteer:
# yarn add puppeteer@next puppeteer-extra
```

## Quickstart

```es6
const puppeteer = require('puppeteer-extra')

// Register plugins through `.use()`
puppeteer.use(require('puppeteer-extra-plugin-anonymize-ua')())
puppeteer.use(require('puppeteer-extra-plugin-font-size')({defaultFontSize: 18}))

(async () => {
  const browser = await puppeteer.launch({headless: false})
  const page = await browser.newPage()
  await page.goto('http://example.com', {waitUntil: 'domcontentloaded'})
  await browser.close()
})()
```

## Plugins

#### [`puppeteer-extra-plugin-stealth`](/packages/puppeteer-extra-plugin-stealth)
- Applies various evasion techniques to make detection of headless puppeteer harder.


#### [`puppeteer-extra-plugin-devtools`](/packages/puppeteer-extra-plugin-devtools)
- Make puppeteer browser debugging possible from anywhere.
- Creates a secure tunnel to make the devtools frontend (**incl. screencasting**) accessible from the public internet


#### [`puppeteer-extra-plugin-flash`](/packages/puppeteer-extra-plugin-flash)
- Allow flash content to run on all sites without user interaction.


#### [`puppeteer-extra-plugin-anonymize-ua`](/packages/puppeteer-extra-plugin-anonymize-ua)
- Anonymizes the user-agent on all pages.
- Supports dynamic replacing, so the browser version stays intact and recent.


#### [`puppeteer-extra-plugin-user-preferences`](/packages/puppeteer-extra-plugin-user-preferences)
- Allows setting custom Chrome/Chromium user preferences.
- Has itself a plugin interface which is used by e.g. [`puppeteer-extra-plugin-font-size`](/packages/puppeteer-extra-plugin-font-size).


> Check out the [packages folder](/packages/) for more plugins.

## Contributing

PRs and new plugins are welcome! :tada: The plugin API for `puppeteer-extra` is clean and fun to use. Have a look the [PuppeteerExtraPlugin](/packages/puppeteer-extra-plugin) base class documentation to get going and check out the [existing plugins](./packages/) (minimal example is the [anonymize-ua](/packages/puppeteer-extra-plugin-anonymize-ua/index.js) plugin) for reference. 

We use a [monorepo](/) powered by [Lerna](https://github.com/lerna/lerna#--use-workspaces) (and yarn workspaces), [ava](https://github.com/avajs/ava) for testing, the [standard](https://standardjs.com/) style for linting and [JSDoc](http://usejsdoc.org/about-getting-started.html) heavily to [auto-generate](https://github.com/transitive-bullshit/update-markdown-jsdoc) markdown [documentation](https://github.com/documentationjs/documentation) based on code. :-)

### Kudos

-   Thanks to [skyiea](https://github.com/skyiea) for [this PR](https://github.com/GoogleChrome/puppeteer/pull/1806) that started the project idea.
-   Thanks to [transitive-bullshit](https://github.com/transitive-bullshit) for [suggesting](https://github.com/berstend/puppeteer-extra/issues/2) a modular plugin design, which was fun to implement.

* * *

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [PuppeteerExtra](#puppeteerextra)
    -   [use](#use)
    -   [launch](#launch)
    -   [plugins](#plugins)
    -   [getPluginData](#getplugindata)
    -   [connect](#connect)
    -   [executablePath](#executablepath)
    -   [defaultArgs](#defaultargs)
    -   [createBrowserFetcher](#createbrowserfetcher)

### [PuppeteerExtra](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L43-L357)

Modular plugin framework to teach `puppeteer` new tricks.

This module acts a drop-in replacement for `puppeteer`.

Allows PuppeteerExtraPlugin's to register themselves and
to extend puppeteer with additional functionality.

Type: `function ()`

Example:

```javascript
const puppeteer = require('puppeteer-extra')
puppeteer.use(require('puppeteer-extra-plugin-anonymize-ua')())
puppeteer.use(require('puppeteer-extra-plugin-font-size')({defaultFontSize: 18}))

(async () => {
  const browser = await puppeteer.launch({headless: false})
  const page = await browser.newPage()
  await page.goto('http://example.com', {waitUntil: 'domcontentloaded'})
  await browser.close()
})()
```

* * *

#### [use](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L63-L79)

Outside interface to register plugins.

Type: `function (plugin): this`

-   `plugin` **PuppeteerExtraPlugin** 

Example:

```javascript
const puppeteer = require('puppeteer-extra')
puppeteer.use(require('puppeteer-extra-plugin-anonymize-ua')())
puppeteer.use(require('puppeteer-extra-plugin-user-preferences')())
const browser = await puppeteer.launch(...)
```

* * *

#### [launch](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L94-L109)

Main launch method.

Augments the original `puppeteer.launch` method with plugin lifecycle methods.

All registered plugins that have a `beforeLaunch` method will be called
in sequence to potentially update the `options` Object before launching puppeteer.

Type: `function (options): Puppeteer.Browser`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Regular Puppeteer options (optional, default `{}`)

* * *

#### [plugins](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L144-L144)

Get all registered plugins.

Type: [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;PuppeteerExtraPlugin>

* * *

#### [getPluginData](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L166-L171)

-   **See: puppeteer-extra-plugin/data**

Collects the exposed `data` property of all registered plugins.
Will be reduced/flattened to a single array.

Can be accessed by plugins that listed the `dataFromPlugins` requirement.

Implemented mainly for plugins that need data from other plugins (e.g. `user-preferences`).

Type: `function (name)`

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Filter data by name property (optional, default `null`)

* * *

#### [connect](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L326-L328)

Regular Puppeteer method that is being passed through.

Type: `function (options)`

-   `options` **{browserWSEndpoint: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), ignoreHTTPSErrors: [boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)}** 

* * *

#### [executablePath](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L335-L337)

Regular Puppeteer method that is being passed through.

Type: `function (): string`

* * *

#### [defaultArgs](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L344-L346)

Regular Puppeteer method that is being passed through.

Type: `function ()`

* * *

#### [createBrowserFetcher](https://github.com/berstend/puppeteer-extra/blob/2fefa134bd3d12f4a1e9f7ed86f44443b38d1098/packages/puppeteer-extra/index.js#L354-L356)

Regular Puppeteer method that is being passed through.

Type: `function (options): PuppeteerBrowserFetcher`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 

* * *
