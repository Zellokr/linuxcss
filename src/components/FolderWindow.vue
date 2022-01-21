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
                        id="header-folder-text"
                        class="ubuntu-font-headline"
                    >Home</span>
                </div>
                <div class="actions-side-bar">
                    <div
                        class="back-forward"
                    />
                    <div class="home-document">
                        <div v-if="status.name === 'proyects'">
                            {{ status.name }}
                            <span v-if="auxProyect"> / {{ auxProyect }}</span>
                        </div>
                    </div>
                </div>
                <div class="body-window">
                    <div
                        v-if="!auxProyect"
                        style="display: flex;"
                    >
                        <div
                            v-for="(proyect,index) in proyects"
                            :key="index"
                            class="folder"
                            @click="getProyect(proyect)"
                        >
                            <img
                                :src="`./folder.png`"
                                alt="carpeta"
                                width="75"
                                height="75"
                            >
                            <span>{{ proyect.name }}</span>
                        </div>
                    </div>
                    <div
                        v-else-if="auxProyect !== null"
                        class="folder"
                    >
                        <img
                            :src="`./readme.png`"
                            alt=""
                            width="75"
                            height="75"
                            @click="openSlimReader"
                        >
                        <span>README</span>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script setup>

import emitter from '../services/emitter'
import { ref } from 'vue'
import { proyects } from '../services/proyects'

const status = ref(null)

const auxProyect = ref(null);

//const slimReader = ref(false);

const getProyect = proyect => {
    auxProyect.value = proyect.name
}

const closeWindow = () =>  {

    emitter.emit('closeIcon', status.value)
    status.value = null
}

const maximizeAction = () =>  {
    status.value.state.maximize = !status.value.state.maximize;
}

const minimizeAction = () =>  {
    emitter.emit('minimize', status.value.state.minimize = !status.value.state.minimize)
}

emitter.on('openFolder', icon =>  status.value = icon );

emitter.on('minimizeFolder', changeMinimize =>  status.value.state.minimize = changeMinimize);

const openSlimReader = () => {

    emitter.emit('insertIconSideBar', { name: 'slim', state: { close: false, minimize: false, maximize: false }, id: 3 })
    emitter.emit('openSlim', { name: 'slim', state: { close: false, minimize: false, maximize: false }, id: 3 })

}

</script>

<style scoped>

  .manual-container{
    display: flex;
    justify-content: center;
    width: 100%;
    height: 100%;
  }

  .window{
    width: 550px;
    height: 500px;
    background: #f2f1ef;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.56) 0px 22px 70px 4px;
    position: relative;
    left: 120px;

  }

  .top-side-window{
      width: 100%;
      height: 40px;
      background: linear-gradient(#504b45 0%,#3c3b37 100%);
      border-top-left-radius: 5px;
      border-top-right-radius: 5px;
      display: flex;
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
  }

  .container-buttons{
    display: flex;
    gap: 5px;
    margin-left: 10px;
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

  .body-folder{
    width: 100%;
    height: 100%;
    display: flex;
    color: white;
    letter-spacing: 0px;
    font-family: 'Ubuntu Mono';
    position: absolute;
    border-bottom-left-radius: 2px;
    border-bottom-right-radius: 2px;
    padding-top: 3px;
    padding-left: 5px;
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

  /* .back-forward{
    display: flex;
    color: #3d3c38;
  }

  .back-forward::before{
    content: '<';
    font-family: 'Ubuntu Mono';
    width: 35px;
    height: 100%;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 36px -18px inset;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #dfdbd2;
    background: #44433e;

  }

    .back-forward::after{
    content: '>';
    width: 35px;
    height: 100%;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 36px -18px inset;
    border-radius: 1px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #dfdbd2;
    background: #44433e;
  } */



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
