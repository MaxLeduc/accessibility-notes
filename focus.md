# Focus

Focus determines where the keyboard events go on the webpage.

Can be accessed by tabbing or clicking.

All pages should be available through the keyboard navigation.

## Tab order

The order focusing happens when we go through the page by tabbing.

Not all elements are inserted in the tab order. For example the header and the paragraphs don't need to be in the tab order since the user doesn't interact with them.

The best way of maintaining a good tab order is to use native HTML elements, for forms for example.

One thing to be cautious about also is that the DOM order will remain the same, event if we change the visual order of elements using CSS. With that in mind, we should always keep a meaningful sequence of elements and tab through elements once in a while to test our tabbing order.

## Tabindex

Property that modifies the tab order.

`tabindex="1"`: element won't be in the tab order.

`tabindex="0"`: element will be in the tab order.

`tabindex="X"` (where X is > 0): element will jump to the front of the tab index. Huge code smell.

Most we should leave the tab index alone, unless it's for something the user will interact with (links, search fields, form elements, buttons), but still, using best practices in terms of tab order should aleviate using `tabindex`.

## Managing focus

Manage focus when it is necessary, for example when a link is pointing to somewhere inside a page or for single page apps when you want to user to be able to go directly to the content where the links are pointing.

1. Make the section header `tabindex="-1"` (to skip it).
1. Using Javascript, listen for when the navigation links are being focused and call the `.focus()` method on the section it should take the user to.

## Skip links

On a webpage, when you press tab after load, it should bring up a link that gives you the option to skip to the main content.

It's a normal link, and it points towards the id of an element on the page. Put that element early in the DOM.

For older browser support, add a `tabindex` of `-1` to the element to tab to.

Skip links should be positionnel absolute at the top of the screen (and actually be off the screen) unless they are focused.

## ARIA design pattern guide

When you are building components that are mimicking the behavior or style of native HTML elements, you need to also ensure they have the same behavior than the native elements.

[Check out this guide for reference](https://www.w3.org/TR/wai-aria-practices/#aria_ex)

## Offscreen content (menus)

If you are tabing around and loose focus, you can log the active element in the browser console by using `document.activeElement` or use the chrome accessbility tools.

To fix that kind of situation where you are loosing focus, add a property of `display: none` or `visibility: hidden` on the element that is causing the issue.

## Keyboard traps

Intentionnally locking the keyboard focus on a particular element. Very useful for modals.

Basically a temporary keyboard trap where the user is cycling between a set number of elements. Can be achieved by Javascript, where our code is listening for certain elements being focused, and when the user is tabbing from the last element, it bring the user back to the first element.
