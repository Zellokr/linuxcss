<template>
    <div class="manual-container">
        <transition
            name="fade"
            mode="out-in"
        >
            <div
                v-if="status"
                v-show="status.state.minimize === false"
                class="window"
                :class="{ 'action-maximize': status.state.maximize}"
            >
                <div class="top-side-window">
                    <span
                        id="header-folder-text"
                        class="ubuntu-font-headline"
                    >Slim Reader</span>
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
                </div>
                <div class="body-slim">
                    <p>
                        Para ver los proyectos creados, vaya a la terminal y ubíquese en la carpeta proyects y monte el proyecto que desee visualizar con el comando <span style="background: yellow;">  npm run build </span>
                    </p>
                    <p>
                        Todos los proyectos han sido creados con VUEJS (HTML, Javascript y CSS nativo)
                    </p>
                    <p>
                        Los proyectos están alojados en mi <a
                            href="https://github.com/Zellokr/"
                            target="_blank"
                        > github </a>
                    </p>
                </div>
            </div>
        </transition>
    </div>
</template>

<script setup>

import emitter from '../services/emitter'
import { ref } from 'vue'
//import { proyects } from '../services/proyects'

const status = ref(null)

const closeWindow = () =>  {

    emitter.emit('closeIcon', status.value)
    status.value = null
}

const maximizeAction = () =>  {
    console.log(status.value)
    status.value.state.maximize = !status.value.state.maximize;
}

const minimizeAction = () =>  {
    emitter.emit('minimize', status.value.state.minimize = !status.value.state.minimize)
}

emitter.on('openSlim', icon =>  status.value = icon );

emitter.on('minimizeSlim', changeMinimize =>  status.value.state.minimize = changeMinimize);


</script>

<style scoped>

  .manual-container{
    display: flex;
    justify-content: space-between;
    width: 100%;
    height: 100%;

  }

  .window{
    width: 500px;
    height: 500px;
    background: #f2f1ef;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.56) 0px 22px 70px 4px;
    position: relative;
    left: 110px;
  }

  .top-side-window{
      width: 100%;
      height: 40px;
      background: linear-gradient(#504b45 0%,#3c3b37 100%);
      border-top-left-radius: 5px;
      border-top-right-radius: 5px;
      display: flex;
      justify-content: flex-end;
      position: relative;
      align-items: center;

  }

  .ubuntu-font-headline{
    font-size: 18px;
    font-style: normal;
    font-variant: normal;
    font-weight: 600;
    color: #d5d0ce;
    letter-spacing: 1px;
    font-family: 'Ubuntu Mono';
    position: absolute;
    text-align: center;
    width: 100%;
    z-index: 0;
  }

  .container-buttons{
    display: flex;
    gap: 5px;
    margin-right: 10px;
    z-index: 1;
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

  .body-slim{
    width: 95%;
    height: 95%;
    display: flex;
    position: absolute;
    flex-direction: column;
    gap: 40px;
    color: black;
    letter-spacing: 0px;
    font-family: 'Arial', sans-serif;
    border-bottom-left-radius: 2px;
    border-bottom-right-radius: 2px;
    padding: 10px;
    margin: 10px;
  }

  #header-folder-text{
    margin-left: 15px;
  }

  .actions-side-bar{
    width: 100%;
    height: 35px;
    background: #3d3c38;
    position: relative;
    display: flex;
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

  .home-document{
    display: flex;
    border-radius: 3px;
    margin-left: 7px;
    padding-left: 5px;
    padding-right: 5px;
    width: auto;
    height: 100%;
    border-top-left-radius: 8%;
    border-bottom-left-radius: 8%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #dfdbd2;
    background: #2b2a27;
  }


  .home-document::before{
    content: '';
  }

    .home-document::after{
      content: '';
  }

    .body-window{
      display: flex;
      width: 100%;
      height: 100%;
    }

    .folder{
      display: flex;
      flex-direction: column;
      text-align: center;
      margin-left: 60px;
      margin-top: 30px;
      color: #3d3c38;
      cursor: pointer;
    }


.fade-enter-active, .fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

</style>
