<template>
    <div class="row">
        <span style="color: #84e338; margin-left: 5px;">
            Kristian@DESKTOP-3QHDLFU:<span style="color: #7592d2;">{{ route }}</span><span style="color: white;">$</span>
        </span>
        <CommandInput />
    </div>
    <div class="response">
        <!-- <CommandResponse /> -->
    </div>
</template>

<script setup>
import CommandInput from './CommandInput.vue';
//import CommandResponse from './CommandResponse.vue';

import emitter from '../services/emitter'
import { ref } from 'vue'

const route = ref('');

emitter.on('command', rut => route.value = rut)

</script>

<style scoped>

.row{
    display: flex;
    flex-direction: flex-col;
  }
.contentInput{
    padding-left: 5px;
    min-height: 17px;
    min-width: 1px;
    outline: 0;
    word-break: break-all;
  }

</style>
