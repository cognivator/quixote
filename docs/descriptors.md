# Quixote API: Descriptors

Descriptors represent some aspect of how the page is rendered, such as an element's width or the position of its top edge.

[Return to the API overview.](api.md)

[Return to the overview README.](../README.md)

**Compatibility Note:** We make every attempt to ensure that descriptors work identically across browsers. If you discover a cross-browser incompatibility that doesn't correspond to an actual, visible difference, please file an issue.

**Pixel Rounding Note:** Browsers handle pixel rounding in different ways. We consider pixel values to be the same if they're within 0.5px of each other. If you have rounding errors that are *greater* than 0.5px, make sure your test browsers are set to a zoom level of 100%. Zooming can exaggerate rounding errors.


### Element Positions and Sizes

```
Stability: 2 - Unstable
```

The position or size of an element. Includes padding and border, but not margin.

Element positions and sizes are available on all [`QElement`](QElement.md) instances.

* `top (`[`PositionDescriptor`](PositionDescriptor.md)`)` The top edge of the element.
* `right (`[`PositionDescriptor`](PositionDescriptor.md)`)` The right edge of the element.
* `bottom (`[`PositionDescriptor`](PositionDescriptor.md)`)` The bottom edge of the element.
* `left (`[`PositionDescriptor`](PositionDescriptor.md)`)` The left edge of the element.
* `center (`[`PositionDescriptor`](PositionDescriptor.md)`)` Horizontal center: midway between the right and left edges.
* `middle (`[`PositionDescriptor`](PositionDescriptor.md)`)` Vertical middle: midway between the top and bottom edges.
* `width (`[`SizeDescriptor`](SizeDescriptor.md)`)` Width of the element.
* `height (`[`SizeDescriptor`](SizeDescriptor.md)`)` Height of the element.

Example: "The logo matches the height of the navbar and is aligned to its right edge."

```javascript
logo.assert({
  height: navbar.height,
  right: navbar.right
});
```


### Viewport Positions and Sizes

```
Stability: 1 - Experimental
```

The viewport is the part of the webpage you can see, not including scrollbars. Viewport position and size descriptors provide information about what parts of the webpage are actually visible. They're useful for comparing to element positions and sizes.

Viewport positions and sizes are available on [`QFrame.viewport()`](QFrame.md).

* `top (`[`PositionDescriptor`](PositionDescriptor.md)`)` The highest visible part of the page.
* `right (`[`PositionDescriptor`](PositionDescriptor.md)`)` The rightmost visible part of the page.
* `bottom (`[`PositionDescriptor`](PositionDescriptor.md)`)` The lowest visible part of the page.
* `left (`[`PositionDescriptor`](PositionDescriptor.md)`)` The leftmost visible part of the page.
* `center (`[`PositionDescriptor`](PositionDescriptor.md)`)` Horizontal center: midway between right and left.
* `middle (`[`PositionDescriptor`](PositionDescriptor.md)`)` Vertical middle: midway between top and bottom.
* `width (`[`SizeDescriptor`](SizeDescriptor.md)`)` Width of the viewport.
* `height (`[`SizeDescriptor`](SizeDescriptor.md)`)` Height of the viewport.

Example: "The cookie disclaimer stretches across the bottom of the viewport."

```javascript
var viewport = frame.viewport();
disclaimer.assert({
  bottom: viewport.bottom,
  width: viewport.width
});
```

**Compatibility Notes:**

* Although there *is* a standard way to get the dimensions of the viewport, and we've confirmed that it works on our [tested browsers](../build/config/tested_browsers.js), it may not be supported properly by all browsers. If you use these descriptors, perform a visual check to make sure they're working as expected, and please report compatibility problems.

* In particular, the current solution for viewport dimensions only works on pages in standards mode. Specifically, they have been tested on pages using `<!DOCTYPE html>`. They do *not* work on pages without a doctype. If support for another doctype is important to you, please let us know by opening an issue.

* Mobile Safari sometimes ignores the `width` and `height` attributes on an iframe, as described in the compatibility note for [`quixote.createFrame()`](quixote.md). This can result in the viewport being larger than expected.


### Page Positions and Sizes

```
Stability: 1 - Experimental
```

The page is everything the user can see or scroll to, not including scrollbars. It's at least as big as the viewport. Page position and size descriptors provide information about the boundaries of the page. They're useful for comparing to element positions and sizes.

Page positions and sizes are available on [`QFrame.page()`](QFrame.md).

* `top (`[`PositionDescriptor`](PositionDescriptor.md)`)` The top of the page.
* `right (`[`PositionDescriptor`](PositionDescriptor.md)`)` The right side of the page.
* `bottom (`[`PositionDescriptor`](PositionDescriptor.md)`)` The bottom of the page.
* `left (`[`PositionDescriptor`](PositionDescriptor.md)`)` The left side of the page.
* `center (`[`PositionDescriptor`](PositionDescriptor.md)`)` Horizontal center: midway between right and left.
* `middle (`[`PositionDescriptor`](PositionDescriptor.md)`)` Vertical middle: midway between top and bottom.
* `width (`[`SizeDescriptor`](SizeDescriptor.md)`)` Width of the page.
* `height (`[`SizeDescriptor`](SizeDescriptor.md)`)` Height of the page.

Example: "The sidebar extends down the left side of the page."

```javascript
var page = frame.page();
sidebar.assert({
  left: page.left,
  height: page.height
});
```

**Compatibility Notes:**

* There is no standard way to get the dimensions of the page. We have implemented a solution that works on our [tested browsers](../build/config/tested_browsers.js), but it may not work on all browsers. If you use these descriptors, perform a visual check to make sure they're working as expected, and please report compatibility problems.

* In particular, the current solution for page dimensions only works on pages in standards mode. Specifically, they have been tested on pages using `<!DOCTYPE html>`. They do *not* work on pages without a doctype. If support for another doctype is important to you, please let us know by opening an issue.


### Common API

All descriptors implement the following method. In most cases, you won't need to call this method directly. Instead, use [`QElement.assert()`](QElement.md) or [`QElement.diff()`](QElement.md).


#### diff()

```
Stability: 2 - Unstable
```

Compare the descriptor to an expected value, which may be another descriptor. Throws an exception if the value isn't comparable to the descriptor.

This is the same as calling [`QElement.diff()`](QElement.md), except that it operates on just one descriptor at a time.

`diff = descriptor.diff(expected)`

* `diff (string)` A human-readable description of any differences found, or an empty string if none.

* `expected (any)` The expected value.

Example: `var diff = element.top.diff(otherElement.top);`
