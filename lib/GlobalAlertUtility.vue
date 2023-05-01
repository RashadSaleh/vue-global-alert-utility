<script>
import {ref} from 'vue';

let alerts = ref([]);
function uuidv4() {
    return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
        (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
    );
}

class Alert {
    constructor({ msg, type }) {
        this.msg = msg;
        this.type = type;

        this.isShowing = false;

        this.id = uuidv4();
    }

    show() {
        alerts.value.push(this);
        this.isShowing = true;
    }

    close() {
        if (!this.isShowing) return;
        else {
            const i = alerts.value.indexOf(this);
            alerts.value.splice(i, 1)
            this.isShowing = false;
        }
    }
}

function alert({ msg, type }) {
    let alert = new Alert({msg, type});
    alert.show();
}

function info(msg) {
    alert({msg, type: "info"});
}

function success(msg) {
    alert({msg, type: "success"});
}

function error(msg) {
    alert({msg, type: "error"});
}
export default {
    info,
    success,
    error,
    data() {
        return {
            alerts
        }
    }
}
</script>

<template>
    <transition-group dir="rtl" tag="div" id="global-alerts-container" name="global-alert">
        <dialog v-for="alert in alerts" :class="['alert', alert.type]" :key="alert.id" open>
            {{ alert.msg }}
            <button @click="alert.close()">×</button>
        </dialog>
    </transition-group>
</template>

<style>
#global-alerts-container dialog.alert {
    position: relative;
    margin-bottom: 10px;
    translate: -50%;
    width: max-content;
    max-width: 90vw;
}

[dir="rtl"] #global-alerts-container dialog.alert,
#global-alerts-container[dir="rtl"] dialog.alert {
    translate: 50%;
}

[dir="rtl"] #global-alerts-container dialog.alert > button,
#global-alerts-container[dir="rtl"] dialog.alert > button {
    left: 0;
    right: initial;
}

#global-alerts-container {
    position: fixed;
    left: 50%;
    top: 5vh;
    width: 0;
}
</style>