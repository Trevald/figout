# Figout
Human friendly layout helper. Inspired by Figmas auto-layout. [View demo](https://trevald.github.io/figout/)

## Parent classes

```html
<div class="
  frame                   <!-- Mandatory, indicates that element should act like a parent -->
  horizontal|vertical     <!-- Mandatory, sets the direction for child elements -->
  left|center|right       <!-- Mandatory, horizontal alignment for children -->
  top|middle|bottom       <!-- Mandatory, vertical alignment for children -->
"></div>                       
```

## Child classes
```html
<div class="
  horizontal-hug-content|horizontal-fill-container
  vertical-hug-content|vertical-fill-container
">
<!--  Hug content will shrink it, fill container will expand it-->
```
