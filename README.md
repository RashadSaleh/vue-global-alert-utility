# Vue Global Alert Utility
A Vue.js global alert utility to replace vanilla JavaScript `alert` 
function with better user and developer experience.

## Demo
A working demo can be found [here](https://rashadsaleh.github.io/vue-global-alert-utility/).

And the demo code is [here](https://github.com/RashadSaleh/vue-global-alert-utility/blob/demo/src/App.vue), 
in case you like the styling used in the demo and
want to adapt it for your own project. *(Please refer to the following
sections for how to properly import the utility in your project)*

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

<style>
/*
Import the basic styles mentioned above.
Omit if you want absolutely 0 styling by default.
*/
@import "vue-global-alert-utility/dist/style.css";
</style>
```

This is where your alerts will be placed in the DOM. 
Normally, you place this at the root component of your app.

Finally, start creating alerts from anywhere in your code:

```vue
<script>
import { GlobalAlertUtility as Alert } from 'vue-global-alert-utility';

Alert.info("This is an info alert!");
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
    border: none;
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
.global-alert-move, /* apply transition to moving elements */
.global-alert-enter-active,
.global-alert-leave-active {
    transition: all 0.5s ease-in-out;
}

.global-alert-enter-from,
.global-alert-leave-to {
    opacity: 0;
    transform: translateY(-30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.global-alert-leave-active {
    position: absolute !important;
}

```

Finally, the basic styles included with the library support RTL layouts out of the box.

## Contributing
Feel free to open an issue to report bugs, ask questions or request features. Pull requests are definitely welcome as well!
