To get dark mode on a pdf in the browser, open up the browser console and paste:

```js
(function(){var el = typeof viewer !== 'undefined' ? viewer : document.body; el.style.filter = 'invert(1) contrast(75%)';})()
```
