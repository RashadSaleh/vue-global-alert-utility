<script setup>
import { GlobalAlertUtility as Alert } from "../lib/main.js";
import { ref } from 'vue';
const msg = ref("This is an alert!");

Alert.info("Welcome to the demo! Use the controls on the left to show a new alert!")
</script>

<template>
  <Alert></Alert>
  alert message: <input v-model="msg">
  <br>
  <button @click="Alert.info(msg)">show info alert</button>
  <br>
  <button @click="Alert.success(msg)">show success alert</button>
  <br>
  <button @click="Alert.error(msg)">show error alert</button>
</template>


<style>
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
</style>

<style>
#global-alerts-container dialog.alert {
    box-shadow: 0 10px 50px #888;
    border: none;
    border-radius: 0.25em;
}

#global-alerts-container dialog.alert.info {
    background-color: white;
}

#global-alerts-container dialog.alert.success {
    background-color: #44FF44;
}

#global-alerts-container dialog.alert.error {
    background-color: #EE4444;
}

#global-alerts-container dialog.alert > button {
    width: 1.5em;
    height: 1.5em;
    padding: 0;
    position: absolute;
    right: 0;
    top: 0;
    line-height: 0;
    font-size: 1em;
    background-color: transparent;
    border: none;
    cursor: pointer;
}
</style>