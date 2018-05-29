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

### [PuppeteerExtra](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L43-L328)

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

#### [use](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L63-L79)

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

#### [launch](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L94-L108)

Main launch method.

Augments the original `puppeteer.launch` method with plugin lifecycle methods.

All registered plugins that have a `beforeLaunch` method will be called
in sequence to potentially update the `options` Object before launching puppeteer.

Type: `function (options): Puppeteer.Browser`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Regular Puppeteer options (optional, default `{}`)

* * *

#### [plugins](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L115-L115)

Get all registered plugins.

Type: [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;PuppeteerExtraPlugin>

* * *

#### [getPluginData](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L137-L142)

-   **See: puppeteer-extra-plugin/data**

Collects the exposed `data` property of all registered plugins.
Will be reduced/flattened to a single array.

Can be accessed by plugins that listed the `dataFromPlugins` requirement.

Implemented mainly for plugins that need data from other plugins (e.g. `user-preferences`).

Type: `function (name)`

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Filter data by name property (optional, default `null`)

* * *

#### [connect](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L297-L299)

Regular Puppeteer method that is being passed through.

Type: `function (options)`

-   `options` **{browserWSEndpoint: [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String), ignoreHTTPSErrors: [boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)}** 

* * *

#### [executablePath](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L306-L308)

Regular Puppeteer method that is being passed through.

Type: `function (): string`

* * *

#### [defaultArgs](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L315-L317)

Regular Puppeteer method that is being passed through.

Type: `function ()`

* * *

#### [createBrowserFetcher](https://github.com/berstend/puppeteer-extra/blob/fecde9acbed91ce2a3edda3f4d12a297fee443a6/packages/puppeteer-extra/index.js#L325-L327)

Regular Puppeteer method that is being passed through.

Type: `function (options): PuppeteerBrowserFetcher`

-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 

* * *
