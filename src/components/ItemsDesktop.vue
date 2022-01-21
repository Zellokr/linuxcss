<template>
    <div
        v-for="(value,key) in icons"
        :key="key"
        class="style-icons"
    >
        <div v-if="value.name !== 'slim'">
            <img

                :src="`./${value.name}.png`"
                alt=""
                width="65"
                height="65"
                style="cursor: pointer"
                @click="openWindow(value.id)"
            >
            <div style="margin-top: 5px;">
                {{ value.name }}
            </div>
        </div>
    </div>
</template>

<script setup>
import emitter from '../services/emitter'
import { icons } from '../services/icons'

const openWindow = id => {
    const icon = JSON.parse(JSON.stringify(icons.find(icon => icon.id === id)))
    icon.state.close = false;
    icon.state.minimize = false;
    if(icon.name === 'terminal'){
        emitter.emit('insertIconSideBar', icon)
        emitter.emit('openTerminal', icon)
    }

    if(icon.name === 'proyects'){
        emitter.emit('insertIconSideBar', icon)
        emitter.emit('openFolder', icon)
    }

    //if(icon.name === 'slim'){
    //emitter.emit('insertIconSideBar', icon)
    //emitter.emit('openSlim', icon)
    //}
}

//emitter.on('actionWindow', e => state = e)

</script>

<style scoped>


.style-icons{
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

</style>
