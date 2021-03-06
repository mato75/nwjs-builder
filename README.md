# nwjs-builder [![Travis CI](https://travis-ci.org/evshiron/nwjs-builder.svg)](https://travis-ci.org/evshiron/nwjs-builder) ![NPM Version](https://img.shields.io/npm/v/nwjs-builder.svg) ![NPM Downloads](https://img.shields.io/npm/dm/nwjs-builder.svg)

A command line utility for building nw.js applications, compatible with `nwjs/nw-builder`, and maybe better.

node.js 4.1+ is required.

[![NPM](https://nodei.co/npm/nwjs-builder.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/nwjs-builder)

## Features

* Use `http://nwjs.io/versions.json` (powered by [evshiron/nwjs-download](https://github.com/evshiron/nwjs-download))
* Use ECMAScript 6
* Support
  * All major versions (listed in `versions.json`)
  * All platforms (win32, linux, darwin)
  * All flavors (normal, sdk, nacl, macappstore)
* Advanced options
  * Build with ffmpeg prebuilt
  * Build without packaging
  * Reinstall node modules for production
  * Replace icon, name, description and etc.
  * ...
* Actively maintained

## Install

```shell
$ npm install evshiron/nwjs-builder -g
```

## Usage

```
# Commands adapted from nwjs-download.

# List versions.
$ nwb list

# Show latest version.
$ nwb latest

# Show stable version.
$ nwb stable

# Show caches.
$ nwb caches

# Commands compatible with nw-builder.

$ nwb nwbuild -h

  Usage: nwbuild [options] [PATH]

  Options:

    -h, --help                                 output usage information
    -v,--version <VERSION>                     The nw.js version, eg. 0.8.4, defaults to the stable version.
    -p,--platforms <PLATFORMS>                 Platforms to build, comma-sperated, eg. win32,win64,osx32,osx64,linux32,linux64, defaults to the current platform.
    -r,--run                                   Runs nw.js at PATH for the current platform.
    -o,--output-dir <DIR_OUTPUT>               The output directory, defaults to PATH's parent.
    -i, --include <DIR_SRC>:<GLOB>[:DIR_DEST]  Include extra files matching GLOB from DIR_SRC to DIR_BUILD/DIR_DEST.
    --with-ffmpeg                              Fetch nwjs-ffmpeg-prebuilt to support .mp3 etc.
    --side-by-side                             Build application with side by side packaging.
    --production                               Reinstall dependencies for production purpose.
    --win-ico <WIN_ICO>                        Specify .ico for Windows build.
    --mac-icns <MAC_ICNS>                      Specify .icns for Mac OS X build.

# Launch application.
$ nwb nwbuild -v 0.14.4-sdk -r ./build/

# Build application for win32,osx64.
$ nwb nwbuild -v 0.14.4-sdk -p win32,osx64 ./build/

# Build application for win32,osx64, with custom icons and without packaging.
$ nwb nwbuild -v 0.14.4-sdk -p win32 --win-ico app.ico --mac-icns app.icns --side-by-side ./build/
```

## Use As Module

`nwjs-builder` is able to work as a node.js module as well. The solution is somewhat tricky, but it works definitely.

```javascript
const NWB = require('nwjs-builder');
NWB.commands.nwbuild(path, options, callback);
```

The above code snippet directly calls the underneath command handler, and the `options` is a fake commander.js `command` object (as all we need are the options). A test named `test-module.js` is provided as a reference.

## Manifest Options

The following manifest options are used to modify executable information, powered by `atom/node-rcedit`.

```
{
    // Normal package.json properties.
    "name": "nwb-test",
    "version": "0.0.1",
    "description": "nwb-test",
    // Additional options.
    "nwjsBuilder": {
        "copyright": "",
        "internalName": "",
        "fileVersion": "",
        "comments": "",
        "companyName": "",
        "legalTrademarks": "",
        "originalFilename": "",
        "privateBuild": "",
        "specialBuild": ""
    }
}
```

## Development

I am still learning about how to form a modern node.js module well. As a result, the project structure might change from time to time.

While new features are added, some existing features might break too.

If anything doesn't work properly, feel free to open issues and provide enough information so that things can be quickly fixed.

PRs and issues are always appreciated.

See also:

* [evshiron/node-flow](https://github.com/evshiron/node-flow)
* [evshiron/nwjs-download](https://github.com/evshiron/nwjs-download)

## License

MIT.
