# iCheck

[![GitHub Version](https://img.shields.io/github/release/gaomingcode/icheck.svg)](https://github.com/gaomingcode/icheck)
[![Packagist Downloads](https://img.shields.io/packagist/dm/gaomingcode/icheck)](https://github.com/gaomingcode/icheck)
[![Github License](https://img.shields.io/github/license/gaomingcode/icheck)](https://github.com/gaomingcode/icheck)

## Installation

### Composer

```
composer require gaomingcode/icheck
```

## ReadMe from Origin
HTML5 allows specifying [indeterminate](http://css-tricks.com/indeterminate-checkboxes/) ("partially" checked) state for checkboxes. iCheck supports this for both checkboxes and radio buttons.

You can make an input indeterminate through HTML using additional attributes (supported by iCheck). Both do the same job, but `indeterminate="true"` may not work in some browsers (like IE7):

```html
indeterminate="true"
<input type="checkbox" indeterminate="true">
<input type="radio" indeterminate="true">

determinate="false"
<input type="checkbox" determinate="false">
<input type="radio" determinate="false">
```

`indeterminate` and `determinate` [methods](#methods) can be used to toggle indeterminate state.

Callbacks
---------

iCheck provides plenty callbacks, which may be used to handle changes.

<table>
  <thead>
    <tr>
      <th>Callback name</th>
      <th>When used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ifClicked</td>
      <td>user clicked on a customized input or an assigned label</td>
    </tr>
    <tr>
      <td>ifChanged</td>
      <td>input's "checked", "disabled" or "indeterminate" state is changed</td>
    </tr>
    <tr>
      <td>ifChecked</td>
      <td>input's state is changed to "checked"</td>
    </tr>
    <tr>
      <td>ifUnchecked</td>
      <td>"checked" state is removed</td>
    </tr>
    <tr>
      <td>ifToggled</td>
      <td>input's "checked" state is changed</td>
    </tr>
    <tr>
      <td>ifDisabled</td>
      <td>input's state is changed to "disabled"</td>
    </tr>
    <tr>
      <td>ifEnabled</td>
      <td>"disabled" state is removed</td>
    </tr>
    <tr>
      <td>ifIndeterminate</td>
      <td>input's state is changed to "indeterminate"</td>
    </tr>
    <tr>
      <td>ifDeterminate</td>
      <td>"indeterminate" state is removed</td>
    </tr>
    <tr>
      <td>ifCreated</td>
      <td>input is just customized</td>
    </tr>
    <tr>
      <td>ifDestroyed</td>
      <td>customization is just removed</td>
    </tr>
  </tbody>
</table>

Use `on()` method to bind them to inputs:

```js
$('input').on('ifChecked', function(event){
  alert(event.type + ' callback');
});
```

`ifCreated` callback should be binded before plugin init.


Methods
-------

These methods can be used to make changes programmatically (any selectors can be used):

```js
// change input's state to 'checked'
$('input').iCheck('check');

// remove 'checked' state
$('input').iCheck('uncheck');

// toggle 'checked' state
$('input').iCheck('toggle');

// change input's state to 'disabled'
$('input').iCheck('disable');

// remove 'disabled' state
$('input').iCheck('enable');

// change input's state to 'indeterminate'
$('input').iCheck('indeterminate');

// remove 'indeterminate' state
$('input').iCheck('determinate');

// apply input changes, which were done outside the plugin
$('input').iCheck('update');

// remove all traces of iCheck
$('input').iCheck('destroy');
```

You may also specify some function, that will be executed on each method call:

```js
$('input').iCheck('check', function(){
  alert('Well done, Sir');
});
```

Feel free to fork and submit pull-request or submit an issue if you find something not working.


Comparison
----------

iCheck is created to avoid routine of reinventing the wheel when working with checkboxes and radio buttons. It provides an expected identical result for the huge number of browsers, devices and their versions. Callbacks and methods can be used to easily handle and make changes at customized inputs.

There are some CSS3 ways available to style checkboxes and radio buttons, like [this one](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-easy-css3-checkboxes-and-radio-buttons/). You have to know about some of the disadvantages of similar methods:

* inputs are keyboard inaccessible, since `display: none` or `visibility: hidden` used to hide them
* poor browser support
* multiple bugs on mobile devices
* tricky, harder to maintain CSS code
* JavaScript is still needed to fix specific issues

While CSS3 method is quite limited solution, iCheck is made to be an everyday replacement covering most of the tasks.


Browser support
---------------

iCheck is verified to work in Internet Explorer 6+, Firefox 2+, Opera 9+, Google Chrome and Safari browsers. Should also work in many others.

Mobile browsers (like Opera mini, Chrome mobile, Safari mobile, Android browser, Silk and others) are also supported. Tested on iOS (iPad, iPhone, iPod), Android, BlackBerry and Windows Phone devices.


Changelog
---------------

## October 10, 2020

* iOS 13 support @markusbroman
* Reformatted changelog @lasseeee
* Fire change event when toggled @rafatmyo

### March 03, 2014

* Better HiDPI screens support @ddctd143

### January 23, 2014 ([v2.0 release candidate](https://github.com/fronteed/icheck/tree/2.x))

* Three ways to set an options: global object (`window.icheck`), data attributes (`<input data-checkedClass="checked"`) and direct JavaScript object (`$(input).icheck({ options })`)
* Huge performance boost (takes less than 1s to customize 1000 inputs)
* Minimized number of function calls (some slow jQuery functions are replaced with a faster vanilla alternatives without using any dependencies)
* AMD module definition support (both for jQuery and Zepto)
* Unblocked native events - iCheck 2.x doesn't stop your newly or past binded events from being processed
* Pointer events support - full support for phones and tablets that use Windows OS (such as Lumia, HP tablets, desktops with a touch screen, etc)
* WebOS and Firefox OS support
* New methods: `$(input).icheck('data')` to get all the options were used for customization (also stores a current states values - `checked`, `disabled` and `indeterminate`), `$('input').icheck('styler')` to get a wrapper div (that's used for customization)
* Better handling of the `indeterminate` state
* Ability to set callbacks in three ways: global object, direct JavaScript object or using bind method (`$(input).on(callback)`)
* Ability to switch off some of the callbacks when you don't need them (global or per input)
* Inline styles dropped - iCheck won't add any inline styles to the elements until it's highly needed (`cursor` or `area` option)
* Fast click support - removes a 300ms click delay on mobile devices without any dependencies (iCheck compatible with the `fastclick` plugin), see the `tap` option
* Ability to ignore customization for the selected inputs using `init` option (if set to `false`)
* Optimized event bindings - iCheck binds only a few global events for the all inputs (doesn't increase on elements addition), instead of a couple for the each customized element
* Doesn't store tons of arbitrary data (event in jQuery or Zepto cache), defines customized elements by specific classnames
* Extra `ins` tag is dropped (less DOM modifications), iCheck wraps each input with a single `div` and doesn't use any extra markup for the any option
* Optimized reflows and repaints on init and state changes
* Better options handling - iCheck will never run a single line of JS to process an options that are off or empty
* Ability to auto customize the ajax loaded inputs without using any extra code (`autoAjax` option, on by default)
* Auto inits on domready using the specified selector (`autoInit` option) - searches for `.icheck` by default. Classnames can be changed using the `window.classes` object
* Memory usage optimization - uses only a few amount of memory (works well on low-memory devices)
* Betters callbacks architecture - these are fired only after changes are applied to the input
* Ability to set a mirror classes between the inputs and assigned labels using the `hoverLabelClass`, `focusLabelClass`, `activeLabelClass`, `checkedLabelClass`, `disabledLabelClass` and `indeterminateLabelClass` options (`mirror` option should be set to `true` to make this happen)
* Fixes some issues of the mobile devices
* Fixes the issues of the wrapper labels, that loose a click ability in some browsers (if no `for` attribute is set)
* Some other options and improvements
* Various bug fixes

Note: extended docs and usage examples will be available later.

### December 19, 2013

* Added Bower support
* Added to jQuery plugin registry

### December 18, 2013

* Added ARIA attributes support (for VoiceOver and others) @myfreeweb
* Added Amazon Kindle support @skinofstars
* Fixed clickable links inside labels @LeGaS
* Fixed lines separation between labels and inputs
* Merged two versions of the plugin (jQuery and Zepto) into one
* Fixed demo links
* Fixed callbacks @PepijnSenders


License
-------
iCheck plugin is released under the [MIT License](http://en.wikipedia.org/wiki/MIT_License). Feel free to use it in personal and commercial projects.