---
<p align="center">
  <h3 align="center">Hi! Do you use webpack?</h3>
</p>
<p align="center">
  I'm currently working on a product that will help you keep track of the assets you're producing and their delivery performance concerns.  Along with reporting those stats right to your GitHub pull requests.
</p>
<p align="center">
  Check it out at <a href="https://packtracker.io">packtracker.io</a> and <a href="https://app.packtracker.io">request early access</a> if you want to help me kick the tires!
</p>

---

# HiDPI Canvas Polyfill

[![Build Status](https://travis-ci.org/jondavidjohn/hidpi-canvas-polyfill.svg?branch=master)](https://travis-ci.org/jondavidjohn/hidpi-canvas-polyfill)

This is a drop-in polyfill to scale canvas appropriately to maintain sharpness
in browsers that currently do not provide the appropriately scaled backing
store to do this automatically.

As of this writing Safari is the only browser that accounts for this.

The goal of this drop-in is to make this behavior consistent accross all browsers,
without having to modify any of your canvas code.

## Scope

Currently this plugin handles most general cross browser drawing functions, but
feel free to send Pull Requests as you find functions you need supported.

If the function simply needs all or some of its arguments multiplied by the ratio,
it should simply require you to add it to the `ratioArgs` object, following the proper
pattern.

It currently leaves images alone, so to retinize images on your canvas, simply
duplicate the getPixelRatio function in your code and divide your image dimensions
by the provided ratio.

```js
var getPixelRatio = function(context) {
    var backingStore = context.backingStorePixelRatio ||
          context.webkitBackingStorePixelRatio ||
          context.mozBackingStorePixelRatio ||
          context.msBackingStorePixelRatio ||
          context.oBackingStorePixelRatio ||
          context.backingStorePixelRatio || 1;

    return (window.devicePixelRatio || 1) / backingStore;
};
```

## Usage

To use this module, simply include it before any of your canvas code

```html
  ...
  <script src=".../dist/hidpi-canvas.min.js"></script>
  <script src=".../your-canvas-stuff.js"></script>
  ...
```

### Bower

This module is also installable via [bower](http://bower.io/)

    bower install hidpi-canvas

## TODO

  - More Complete context function coverage
  - Figure out how to write tests for this type of thing

## Development

See [CONTRIBUTING.md](https://github.com/jondavidjohn/hidpi-canvas-polyfill/blob/develop/CONTRIBUTING.md)

