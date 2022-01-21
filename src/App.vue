<script setup>
import TerminalLinux from './components/TerminalLinux.vue';
import ItemsDesktop from './components/ItemsDesktop.vue';
import SideBar from './components/SideBar.vue';
import FolderWindow from './components/FolderWindow.vue';
import SlimReader from './components/SlimReader.vue';

</script>

<template>
    <div class="background-wallepaper">
        <SideBar />
        <div class="container-items">
            <ItemsDesktop />
        </div>
        <div class="items">
            <TerminalLinux />
            <FolderWindow />
            <SlimReader />
        </div>
    </div>
</template>

<style>

*{
  padding: 0;
  margin: 0;

}

#app {
  font-family: 'Ubuntu Mono';
  color: white;
  font-size: 15px;
  font-style: normal;
  font-variant: normal;
  font-weight: 600;
  color: #d5d0ce;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}

.background-wallepaper{
  background-image: url('./assets/ubuntu-wallepaper.jpg');
  background-repeat: no-repeat;
  width: 100vw;
  height: 100vh;
  overflow: hidden;

}


 /* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
  .background-wallepaper{overflow: hidden;}
}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {
  .background-wallepaper{overflow: hidden;}
}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {
  .background-wallepaper{overflow: auto;}
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {
  .background-wallepaper{overflow: auto;}
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
.background-wallepaper{overflow: auto;}
}


.container-items{
  display: inline-block;
  position: relative;
  left: 170px;
  top: 35px;

}

.items{
  display: flex;
  justify-content: center;


}

@font-face{
    font-family: "Pretendo";
    src: local("Pretendo"),
        url(./assets/fonts/Pretendo.ttf) format(truetype)
}

@font-face{
    font-family: "Ubuntu";
    src: local("Ubuntu"),
        url(./assets/fonts/Ubuntu-Regular.ttf) format(truetype)
}


</style>
