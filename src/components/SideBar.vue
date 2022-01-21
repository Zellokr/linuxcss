<template>
    <div class="side-bar">
        <transition-group
            name="bounce"
            tag="div"
        >
            <div
                v-for="(value,index) in iconList"
                :key="index"
            >
                <img
                    v-if="iconList.length > 0"
                    :src="`./${value.name}.png`"
                    alt=""
                    width="65"
                    height="65"
                    style="cursor: pointer; padding-top: 30px;"
                    @click="changeStatus(value)"
                >
            </div>
        </transition-group>
    </div>
</template>

<script setup>
import emitter from '../services/emitter'
import { ref } from 'vue'

const iconList = ref([]);

const statusWindow = ref(false)

emitter.on('insertIconSideBar', icon => {
    if(!iconList.value.some(item => icon.id === item.id))
        iconList.value.push(icon);
});

emitter.on('closeIcon', icon =>  {
    const index = iconList.value.map(icon => icon.id).indexOf(icon.id);
    if (index > -1)
        iconList.value.splice(index, 1)

})

emitter.on('minimize', state =>  statusWindow.value = state);

const changeStatus = value => {
    if(value.name === 'terminal')
        emitter.emit('minimizeTerminal', statusWindow.value = !statusWindow.value)

    if(value.name === 'proyects')
        emitter.emit('minimizeFolder', statusWindow.value = !statusWindow.value)

    if(value.name === 'slim')
        emitter.emit('minimizeSlim', statusWindow.value = !statusWindow.value)
}

</script>

<style scoped>

.side-bar{
    width: 5%;
    height: 100%;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.5);
    background: rgba(0,0,0,0.65);
    position: absolute;
    display: flex;
    justify-content: start;
    align-items: center;
    flex-direction: column;

}
.bounce-enter-active {
  animation: bounce-in .2s ease-out both;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>
