# Eleventy Plugin Safe External Links

![npm version](https://badge.fury.io/js/%40hirusi%2Feleventy-plugin-safe-external-links.svg)
![npm downloads](https://img.shields.io/npm/dw/@hirusi/eleventy-plugin-safe-external-links)

[Eleventy plugin](https://www.11ty.dev/docs/plugins/) ensuring that external links always contain `rel="noopener"`, `rel="noreferrer"`, which are [potentially unsafe otherwise](https://web.dev/external-anchors-use-rel-noopener/).

## Installing

```bash
npm install @hirusi/eleventy-plugin-safe-external-links
```

This has only been tested with Eleventy 0.11.0 and would ideally be kept up to date with only future releases of Eleventy.

## Usage

```js
const safeExternalLinks = require("@hirusi/eleventy-plugin-safe-external-links")

module.exports = function (eleventyConfig) {

  eleventyConfig.addPlugin(safeExternalLinks, {
    pattern: "https{0,1}://", // RegExp pattern for external links
    noopener: true, // Whether to include noopener
    noreferrer: false, // Whether to include noreferrer
    files: [
      // What output file extensions to work on
      ".html",
    ],
  });
  
}
```

Including noreferrer in your external links is optional. Please see [more on this in an article by pointjupiter.com here](https://pointjupiter.com/what-noopener-noreferrer-nofollow-explained/), as pointed out by [@grempe](https://github.com/grempe/). As always, please do your own research as well and make an informed choice. 😊

## Differences from chromeos/static-site-scaffold-modules/modules/eleventy-plugin-safe-external-links

* This is not a mono-repo. Easier to manage and release updates.
* Ignores files where `permalink` is set to `false`.
* Fixes an issue where the plugin would empty everything but the body of the page `content`. ([see issue with cheerio](https://github.com/cheeriojs/cheerio/issues/1031))
* Adds `_blank` target to external links, __unless `noopener` is set to false.__
* Adds `_blank` target to external links already carrying `noopener` rel __(ignores `noopener` option)__
* Updated tests.
* Updated README.

## Versioning

I intend to keep this up to date with the original repo as best as I can. The patch and minor fields from the source repo would be combined - `0.1.4` would change to `0.14.0`. The patch field then would reflect my changes on top of it for that minor release - `0.14.1`.
