# Quixote Roadmap

## Release Ideas

* **✔ v0.1** Basic DOM manipulation; raw position and style information
* **✔ v0.2** "Cooked" absolute position info; initial assertion API
* **✔ v0.3** Positioning relative to other elements
* **✔ v0.4** Advanced positioning (middle, center, height, width, arithmetic, fractions)
* **✔ v0.5** API hardening
* **✔ v0.6** Responsive design
* **✔ v0.7** Page and viewport assertions
* **v0.8, v0.9** Dogfooding and real-world usage (more dogfooding releases to come)
* Initial "cooked" styling (colors? contrast (fg color vs. bg color?))
* ...more TBD


## Current Feature: Documentation Update (0.10 release)

* ✔ Revise readme
* Revise API docs
* Revise contributor docs
* Add overview docs
	* *Performance note:* In some cases (specifically, Safari on Mac OS X), running Quixote while the browser is hidden causes very slow tests. If you have trouble with slow tests, make sure your browser windows are visible.
* Create example project
* Document work-around for cross-origin restrictions (using a proxy, such as in Karma)
* Document IE font caching issue: if you only change a font size in a CSS file, then IE 9 and 11 (and more?) may not pick it up on the next test run.
* Release 0.10


## To Do: Readme

* Done


## Dogfooding Notes

* Provide a better way of integrating with standard assertion libraries?
* Provide better error message when cross-origin 'src' provided to quixote.createFrame
* Add workaround for IE 8 not working with `frame.add("<style>...</style>")` (addAll? browser feature detect? Need to check if there's no way to insert styles into the document, or if it just doesn't like the way `add()` works.)  
* Add `QElement.add()` and `QElement.remove()`?


## Future Features

* Z-ordering
* Support multiple assertions? (e.g., `top.diff([bar.left, baz.right]);`)
* Distances or Spans? (e.g., height of menu is equal to distance between logo top and headline bottom)
  * Could width and height be reimplemented as a Span? Would a Span have a center, for example?
    * Even if it could, would it be a good idea?
    * E.g., Me.width = function() { this.left.to(this.right) };
* Investigate re-enabling URL checking (issue #4)
* Consider how to support less-than, greater-than, etc.
  * Use case: "the bottom edge of 'foo' is above the fold (600px)".
  * .max and .min?  `foo.assert({ bottom: top.plus(600).max });`   `foo.assert({ bottom: q.max(600) });`

