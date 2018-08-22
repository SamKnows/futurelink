# futurelink

> Calculates the deceleration of the cursor to predict when a link is about to be clicked.

## Install

```
$ npm install --save futurelink
```

## Usage

```js
var futurelink = require('futurelink');

futurelink({
  links: document.querySelectorAll('a'),
  future: function (link) {
    // `link` is probably going to be clicked soon
    // Preload some images, if you can!
  },
  
  // These also exist, but aren't usually needed:
  hover: function (link) {},
  click: function (link) {}
})
```

Pass it an array or NodeList of elements, and when the cursor is approaching one of those elements, the `future` callback will be fired with the element in question as an argument. `future` will only be called once per element.

The links are read directly from the options object, so if you want to update the links being watched (say, because you want to watch some elements newly added to the DOM), you can do this:

```js
var options = {
  links: document.querySelectorAll('a'),
  future: function (link) {}
};

futurelink(options);

router.afterEach(function () {
  options.links = document.querySelectorAll('a');
});
```

### Disabling for sections of the page / individual links

futurelink won't look at links that have a `no-futurelink` class on them or one of their parent elements. It also only looks at internal links.

```html
<div class="no-futurelink">
  <a href="/foo-bar">Futurelink won't tell you about this link</a>
</div>

<a href="/bar-foo" class="no-futurelink">It won't tell you about this one either</a>
```

### Removing futurelink from the page

If you want to completely remove futurelink, it returns a `teardown` function that you can call:

```js
var teardown = futurelink(options);

// Later…

teardown();
```

Now the event listeners will be removed and futurelink won't tell you when links are about to be clicked anymore.

## How effective is it

On samknows.com, it speeds up non-initial page loads by an average of 870ms.

## How does it work?

You can see an article about that on the [SamKnows Medium](https://blog.samknows.com/intelligent-page-preloading-with-futurelink-c1de25449dee).

## Usage with frameworks

- [vue-futurelink](https://github.com/SamKnows/vue-futurelink)

## License

Released under the MIT license.
