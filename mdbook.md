
The following changes need to be made to mdbook...

To make the sidebar always display.

src/theme/index.hbs

```js
var sidebar = 'hidden';
var sidebar = 'visible';
```

src/theme/css/variables.css

/* Globals */

```css
:root {
--sidebar-width: 300px;
--sidebar-width: 200px;
```
