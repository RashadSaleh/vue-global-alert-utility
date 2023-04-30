# Vue Global Alert Utility

## Why? 
This package provides a global alert utility for your vue projects.

The idea is to replace the native JavaScript `alert` 
function with something more user and developer friendly, 
yet retain as much of the simplicity as possible.

The library primarily provides functionality without theming, 
but it is "theming ready". The only exception is that alerts are
by default placed at the top of the page and centered horizontally, 
and a small margin at the bottom of each alert is applied (which you can override).

So, while `alert` is handy in that 
it is available everywhere and is simple to use --

1. It is impossible to theme
2. It is awkward for the user to interact with
3. Cannot show more than one alert at the same time

This utility solves all 3 problems.

## Usage

Install the package:

```
pnpm install vue-global-alert-utility
```

Place the component once somewhere in the code:

```vue
<script>
import { GlobalAlertUtility } from 'vue-global-alert-utility';
</script>

<template>
  ...
    <GlobalAlertUtility />
  ...
</template>
```

This is where your alerts will be placed in the DOM. 
Normally, you place this at the root component of your app.

Finally, start creating alerts from anywhere in your code:

```vue
<script>
import { GlobalAlertUtility as Alert } from 'vue-global-alert-utility';

Alert.info("This is a success alert!");
Alert.success("This is a success alert!");
Alert.error("This is an error alert!");
</script>
```

Without theming, you will notice that all three alerts are displayed 
the same. Next we discuss how you can customize each one of them to look
just the way you want.

## Theming

Global alerts are theming ready. Every aspect of the 
alert is easily accessible through CSS selectors.

To style all alerts of any type, use the selector:
```css
#global-alerts-container dialog.alert {
    border-radius: 5px;
}
```

To style a `success`, `error` or `info` alert, use the selectors:
```css
#global-alerts-container dialog.alert.success {
    background-color: green;
}
#global-alerts-container dialog.alert.error {
    background-color: red;
}
#global-alerts-container dialog.alert.info {
    background-color: lightblue;
}
```

To style the close button for an alert:
```css
#global-alerts-container dialog.alert > button {
    background-color: white;
    color: red;
}
```

You can also add transitions easily for your alerts, since the alerts
are already wrapped for you inside a:
```vue
<transition-group tag="div" id="global-alerts-container" name="global-alert">
```
element.

Which means you can do something like this:
```css
.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease-in-out;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateY(-30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
    position: absolute !important;
}
```