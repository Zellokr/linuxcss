<template>
    <span
        ref="terminalInput"
        :contenteditable="triggerContentEditable"
        class="contentInput"
        @blur="alwaysFocus"
        @keydown.enter.prevent="insertCommand"
    />
</template>

<script setup>

import { ref } from 'vue'
import emitter from '../services/emitter'

const terminalInput = ref(null);

const triggerContentEditable = ref(true);

setTimeout(function() {
    terminalInput.value.focus();
}, 10);

const alwaysFocus = () => {
    setTimeout(() => {
        if(terminalInput.value !== null)
            terminalInput.value.focus();
    },
    100)
}

const insertCommand = event => {
    if(event.code === 'Enter')
        emitter.emit('enterCommand', [event.target.textContent, terminalInput.value, triggerContentEditable.value = false])

}

emitter.on('updateContentEditable', state => triggerContentEditable.value = state)


</script>

<style scoped>

.contentInput{
    padding-left: 5px;
    min-height: 17px;
    min-width: 1px;
    outline: 0;
    word-break: break-all;
  }



</style>
