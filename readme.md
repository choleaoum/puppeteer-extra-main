# puppeteer-extra

## Examples

```bash
node examples/foo.js
# with debug logs
DEBUG=puppeteer-extra,puppeteer-extra-plugin:* node examples/foo.js
```

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

### [PuppeteerExtra](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L43-L289)

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

#### [use](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L63-L79)

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

#### [launch](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L92-L103)

Main launch method.

Augments the original `puppeteer.launch` method with plugin lifecycle methods.

It'll call all loaded plugins that have a `beforeLaunch` method
in sequence to potentially update the options Object before launch.

Type: `function (options): Puppeteer.Browser`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Regular Puppeteer options (optional, default `{}`)

* * *

#### [plugins](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L110-L110)

Get all loaded plugins.

Type: [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;PuppeteerExtraPlugin>

* * *

#### [getPluginData](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L131-L136)

Collects the exposed `data` property of all loaded plugins.
Will be reduced/flattened to a single array.

Can be accessed by plugins that listed the `dataFromPlugins` requirement.

Implemented mainly for plugins that need data from other plugins (e.g. `user-preferences`).

Type: `function (name)`

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Filter data by name property (optional, default `null`)

* * *

#### [connect](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L258-L260)

Regular Puppeteer method that is being passed through.

Type: `function (options)`

-   `options` **{browserWSEndpoint: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), ignoreHTTPSErrors: [boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)}** 

* * *

#### [executablePath](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L267-L269)

Regular Puppeteer method that is being passed through.

Type: `function (): string`

* * *

#### [defaultArgs](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L276-L278)

Regular Puppeteer method that is being passed through.

Type: `function ()`

* * *

#### [createBrowserFetcher](https://github.com/berstend/puppeteer-extra/blob/aef617794c228564231f021105691273a0297b1c/packages/puppeteer-extra/index.js#L286-L288)

Regular Puppeteer method that is being passed through.

Type: `function (options): PuppeteerBrowserFetcher`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 

* * *
