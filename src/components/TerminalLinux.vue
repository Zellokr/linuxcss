<template>
    <div

        class="manual-container"
    >
        <transition
            name="fade"
            mode="out-in"
        >
            <div
                v-if="status"
                v-show="status.state.minimize === false"
                class="terminal"
                :class="{ 'action-maximize': status.state.maximize}"
            >
                <div class="top-side-terminal">
                    <div class="container-buttons">
                        <div
                            class="close"
                            @click="closeWindow"
                        >
                            <span>&#10005;</span>
                        </div>
                        <div
                            class="minimize"
                            @click="minimizeAction"
                        >
                            <span>&#9472;</span>
                        </div>
                        <div
                            class="maximize"
                            @click="maximizeAction"
                        >
                            <span>&#9723;</span>
                        </div>
                    </div>
                    <span
                        id="header-terminal-text"
                        class="ubuntu-font-headline"
                    >kristian@DESKTOP-3QHDLFU:~</span>
                </div>
                <div

                    class="body-terminal"
                >
                    <CommandLine
                        v-for="line in lines"
                        :key="line"
                    />
                </div>
            </div>
        </transition>
    </div>
</template>

<script setup>

import emitter from '../services/emitter'
import { ref } from 'vue'
import CommandLine from './CommandLine.vue';

const status = ref(null);

const lines = ref(1);

const route = ref('~')

const response = ref(false);

const closeWindow = () =>  {
    emitter.emit('closeIcon', status.value)
    status.value = null
}

const maximizeAction = () =>  status.value.state.maximize = !status.value.state.maximize;

const minimizeAction = () =>  emitter.emit('minimize', status.value.state.minimize = !status.value.state.minimize)

emitter.on('enterCommand', array => {
    if(array[0] === 'clear'){
        lines.value = 0;

        setTimeout(() => {
            if(array[1] !== null)
                array[1].focus()
        },
        100)
        emitter.emit('updateContentEditable', array[2] = true)
    }
    if(array[0] === 'cd proyects'){
        lines.value = 0;
        route.value = '/home/kristian/proyects';
        emitter.emit('command', route.value)
    }
    if(array[0] === 'cd gameboycss'){
        lines.value = 0;
        route.value = '/home/kristian/proyects/gameboycss';
    }
    if(array[0] === 'cd api-betting')
    {
        lines.value = 0;
        route.value = '/home/kristian/proyects/api-betting';
    }
    if(array[0] === 'npm run dev'){
        lines.value = 0;
        window.open('https://www.codexworld.com', '_blank');
    }
    if(array[0] === 'cd ..')
    {
        lines.value = 0;
        route.value = '~';
    }
    if(array[0] === 'ls')
    {

        response.value = "true"
    }

    setTimeout(() => lines.value += 1, 100);
});

emitter.on('openTerminal', icon =>  status.value = icon);

emitter.on('minimizeTerminal', changeMinimize =>  status.value.state.minimize = changeMinimize);


</script>

<style scoped>

  .manual-container{
    display: flex;
    justify-content: center;
    width: 100%;
    height: 100%;
  }


  .terminal{
    width: 600px;
    height: 500px;
    background: #300924;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.56) 0px 22px 70px 4px;
    position: relative;
    right: -150px;



  }

  .top-side-terminal{
      width: 100%;
      height: 35px;
      background: linear-gradient(#504b45 0%,#3c3b37 100%);
      border-top-left-radius: 5px;
      border-top-right-radius: 5px;
      display: flex;
      position: relative;
      align-items: center;

  }

  .ubuntu-font-headline{
    font-size: 15px;
    font-style: normal;
    font-variant: normal;
    font-weight: 600;
    color: #d5d0ce;
    font-family: 'Ubuntu Mono';
    transform: translateX(6px);
  }

  .container-buttons{
    display: flex;
    gap: 5px;
    margin-left: 10px;
  }

  .response{
    margin-left: 5px;
  }

  .close{
    width: 20px;
    height: 20px;
    background: linear-gradient(#f37458 0%, #de4c12 100%);
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    text-shadow: 0px 1px 0px rgba(255,255,255,0.2);
    box-shadow: 0px 0px 1px 0px #41403A, 0px 1px 1px 0px #474642;

  }

  .minimize{
    width: 20px;
    height: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    background: linear-gradient(#7d7871 0%, #595953 100%);
    text-shadow: 0px 1px 0px rgba(255,255,255,0.2);
    box-shadow: 0px 0px 1px 0px #41403A, 0px 1px 1px 0px #474642;
    border-radius: 50%;
  }

  .maximize{
    width: 20px;
    height: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    background: linear-gradient(#7d7871 0%, #595953 100%);
    text-shadow: 0px 1px 0px rgba(255,255,255,0.2);
    box-shadow: 0px 0px 1px 0px #41403A, 0px 1px 1px 0px #474642;
    border-radius: 50%;
  }


  .maximize span, .minimize span, .close span {
    color: #4a3d31;
    font-family: 'Ubuntu', sans-serif;
  }

  .action-maximize{
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: hidden;

  }

  .body-terminal{
    width: 100%;
    height: 92%;
    color: white;
    letter-spacing: 0px;
    font-family: 'Ubuntu Mono';
    position: absolute;
    border-bottom-left-radius: 2px;
    border-bottom-right-radius: 2px;
    padding-top: 3px;
    overflow-y: auto;


  }


  #header-terminal-text{
    margin-left: 15px;
  }


.fade-enter-active, .fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

</style>
