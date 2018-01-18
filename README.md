<a href="https://plot.ly/javascript/"><img src="http://images.plot.ly/logo/plotlyjs-logo@2x.png" height="70"></a>

[![npm version](https://badge.fury.io/js/plotly.js.svg)](https://badge.fury.io/js/plotly.js)
[![circle ci](https://circleci.com/gh/plotly/plotly.js.png?&style=shield&circle-token=1f42a03b242bd969756fc3e53ede204af9b507c0)](https://circleci.com/gh/plotly/plotly.js)
[![MIT License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://github.com/plotly/plotly.js/blob/master/LICENSE)

Built on top of [d3.js](http://d3js.org/) and [stack.gl](http://stack.gl/),
plotly.js is a high-level, declarative charting library. plotly.js ships with over 20
chart types, including scientific charts, 3D graphs, statistical charts, SVG maps, financial charts,
and more.

<p align="center">
    <a href="https://www.plot.ly/javascript" target="_blank">
    <img src="https://raw.githubusercontent.com/cldougl/plot_images/add_r_img/plotly_2017.png">
</a></p>

[Contact us](https://plot.ly/products/consulting-and-oem/) for Plotly.js consulting, dashboard development, application integration, and feature additions.

## Table of contents

* [Quick start options](#quick-start-options)
* [Modules](#modules)
* [Bugs and feature requests](#bugs-and-feature-requests)
* [Documentation](#documentation)
* [Contributing](#contributing)
* [Community](#community)
* [Clients for R, Python, Node, and MATLAB](#clients-for-r-python-node-and-matlab)
* [Creators](#creators)
* [Copyright and license](#copyright-and-license)


## Quick start options

#### Download the latest release
[Latest Release on Github](https://github.com/plotly/plotly.js/releases/)

and use the plotly.js `dist` file(s). More info [here](https://github.com/plotly/plotly.js/blob/master/dist/README.md).

#### Clone the repo

```bash
git clone https://github.com/plotly/plotly.js.git
```

and use the plotly.js `dist` file(s).

#### Install with `npm`

```bash
npm install plotly.js
```

and require plotly.js using CommonJS as `var Plotly = require('plotly.js');` or use the plotly.js `dist` file(s).

#### Use the plotly.js CDN hosted by Fastly
```html
<!-- Latest compiled and minified plotly.js JavaScript -->
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>

<!-- OR use a specific plotly.js release (e.g. version 1.5.0) -->
<script src="https://cdn.plot.ly/plotly-1.5.0.min.js"></script>

<!-- OR an un-minified version is also available -->
<script src="https://cdn.plot.ly/plotly-latest.js"></script>
```

and use the `Plotly` object in the window scope.

##### Read the [Getting started page](https://plot.ly/javascript/getting-started/) for more examples.

## Modules

Starting in `v1.15.0`, plotly.js also ships with several _partial_ bundles (more info [here](https://github.com/plotly/plotly.js/blob/master/dist/README.md#partial-bundles)).

If you would like to manually pick which plotly.js modules to include, you can create a *custom* bundle by using `plotly.js/lib/core`, and loading only the trace types that you need (e.g. `pie` or `choropleth`). The recommended way to do this is by creating a *bundling file*:

```javascript
// in custom-plotly.js
var Plotly = require('plotly.js/lib/core');

// Load in the trace types for pie, and choropleth
Plotly.register([
    require('plotly.js/lib/pie'),
    require('plotly.js/lib/choropleth')
]);

module.exports = Plotly;
```

Then elsewhere in your code:

```javascript
var Plotly = require('./path/to/custom-plotly');
```

To learn more about the plotly.js module architecture, refer to our [modularizing monolithic JS projects](https://plot.ly/javascript/modularizing-monolithic-javascript-projects/) post.

#### Non-ascii characters

Important: the plotly.js code base contains some non-ascii characters. Therefore, please make sure to set the `charset` attribute to `"utf-8"` in the script tag that imports your plotly.js bundle. For example:

```html
<script src="my-plotly-bundle.js" charset="utf-8"></script>
```


#### Building plotly.js with Webpack

For plotly.js to build with Webpack you will need to install [ify-loader@v1.1.0+](https://github.com/hughsk/ify-loader) and add it to your `webpack.config.json`. This adds Browserify transform compatibility to Webpack which is necessary for some plotly.js dependencies.

A repo that demonstrates how to build plotly.js with Webpack can be found [here](https://github.com/rreusser/plotly-webpack). In short add `ify-loader` to the `module` section in your `webpack.config.js`:
```js
...
    module: {
        rules: [
            {
                test: /\.js$/,
                loader: 'ify-loader'
            }
        ]
    },
...
```

#### Building plotly.js with Angular CLI

Currently Angular CLI use Webpack under the hood to bundle and build your Angular application.
Sadly it doesn't allow to override its Webpack config, and therefore to use the plugin mentioned in [Building plotly.js with Webpack](#building-plotlyjs-with-webpack).
Without this plugin your build will fail when it tries to build glslify for GLSL plots.

Currently 2 solutions exists to circumvent this issue :
1) If you need to use GLSL plots, you can create a Webpack config from your Angular CLI projet with [ng eject](https://github.com/angular/angular-cli/wiki/eject).
This will allow you to follow the instructions regarding Webpack.
2) If you don't need to use GLSL plots, you can make a custom build containing only the required modules for your plots.
The clean way to do it with Angular CLI is not the method described in [Modules](#modules) but the following :
```typescript
// in the Component you want to create a graph
import * as Plotly from 'plotly.js';
```

```json
// in src/tsconfig.app.json
// List here the modules you want to import
// this exemple is for scatter plots
{
    "compilerOptions": {
        "paths": {
            "plotly.js": [
                "../node_modules/plotly.js/lib/core.js",
                "../node_modules/plotly.js/lib/scatter.js"
            ]
        }
    }
}
```

## Bugs and feature requests

Have a bug or a feature request? Please first read the [issues guidelines](https://github.com/plotly/plotly.js/blob/master/CONTRIBUTING.md#opening-issues).

## Documentation

Official plotly.js documentation is hosted on [plot.ly/javascript](https://plot.ly/javascript).

These pages are generated by the Plotly [documentation repo](https://github.com/plotly/documentation/tree/gh-pages) built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages.
For more info about contributing to Plotly documentation, please read through [contributing guidelines](https://github.com/plotly/documentation/blob/source/Contributing.md).

You can also suggest new documentation examples by submitting a [Codepen](http://codepen.io/tag/plotly/) on community.plot.ly with tag [`plotly-js`](http://community.plot.ly/c/plotly-js).

## Contributing

Please read through our [contributing guidelines](https://github.com/plotly/plotly.js/blob/master/CONTRIBUTING.md). Included are directions for opening issues, using plotly.js in your project and notes on development.

## Community

* Follow [@plotlygraphs](https://twitter.com/plotlygraphs) on Twitter for the latest Plotly news.
* Follow [@plotly_js](https://twitter.com/plotly_js) on Twitter for plotly.js release updates.
* Implementation help may be found on community.plot.ly (tagged [`plotly-js`](http://community.plot.ly/c/plotly-js)) or
  on Stack Overflow (tagged [`plotly`](https://stackoverflow.com/questions/tagged/plotly)).
* Developers should use the keyword `plotly` on packages which modify or add to the functionality of plotly.js when distributing through [npm](https://www.npmjs.com/browse/keyword/plotly).
* Direct developer email support can be purchased through a [Plotly Support Plan](https://support.plot.ly/libraries/javascript).

## Versioning

This project is maintained under the [Semantic Versioning guidelines](http://semver.org/).

See the [Releases section](https://github.com/plotly/plotly.js/releases) of our GitHub project for changelogs for each release version of plotly.js.

## Clients for R, Python, Node, and MATLAB

Open-source clients to the plotly.js APIs are available at these links:

|   | GitHub repo | Getting started |
|---|--------|---------|
|**R / RStudio**| [ropensci/plotly](https://github.com/ropensci/plotly) | [plot.ly/r/getting-started](https://plot.ly/r/getting-started) |
|**Python / Pandas / IPython notebook**| [plotly/plotly.py](https://github.com/plotly/plotly.py) | [plot.ly/python/getting-started](https://plot.ly/python/getting-started) |
|**MATLAB**| [plotly/matlab-api](https://github.com/plotly/matlab-api) | [plot.ly/matlab/getting-started](https://plot.ly/matlab/getting-started) |
|**node.js / Tonicdev / Jupyter notebook**| [plotly/plotly-notebook-js](https://github.com/plotly/plotly-notebook-js) | |
|**node.js cloud client**| [plotly/plotly-nodejs](https://github.com/plotly/plotly-nodejs) | [plot.ly/nodejs/getting-started](https://plot.ly/nodejs/getting-started) |
|**Julia**| [plotly/Plotly.jl](https://github.com/plotly/Plotly.jl) | [plot.ly/julia/getting-started](https://plot.ly/julia/getting-started) |

plotly.js charts can also be created and saved online for free at [plot.ly/create](https://plot.ly/create).

## Creators

|   | Github | Twitter |
|---|--------|---------|
|**Alex C. Johnson**| [@alexcjohnson](https://github.com/alexcjohnson) | |
|**Étienne Tétreault-Pinard**| [@etpinard](https://github.com/etpinard) | [@etpinard](https://twitter.com/etpinard) |
|**Mikola Lysenko**| [@mikolalysenko](https://github.com/mikolalysenko) | [@MikolaLysenko](https://twitter.com/MikolaLysenko) |
| **Dmitry Yv.** | [@dy](https://github.com/dy) | [@DimaYv](https://twitter.com/dimayv)|
|**Ricky Reusser**| [@rreusser](https://github.com/rreusser) | [@rickyreusser](https://twitter.com/rickyreusser) |
|**Robert Monfera**| [@monfera](https://github.com/monfera) | [@monfera](https://twitter.com/monfera) |
|**Nicolas Riesco**| [@n-riesco](https://github.com/n-riesco) | |
|**Miklós Tusz**| [@mdtusz](https://github.com/mdtusz) | [@mdtusz](https://twitter.com/mdtusz)|
|**Chelsea Douglas**| [@cldougl](https://github.com/cldougl) | |
|**Ben Postlethwaite**| [@bpostlethwaite](https://github.com/bpostlethwaite) | |
|**Chris Parmer**| [@chriddyp](https://github.com/chriddyp) | |
|**Alex Vados**| [@alexander-daniel](https://github.com/alexander-daniel) | |


## Copyright and license

Code and documentation copyright 2018 Plotly, Inc.

Code released under the [MIT license](https://github.com/plotly/plotly.js/blob/master/LICENSE).

Docs released under the [Creative Commons license](https://github.com/plotly/documentation/blob/source/LICENSE).
