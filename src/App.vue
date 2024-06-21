<script >

import Game from "./components/Game.vue";
import Header from "./components/Header.vue";

export default {
  name:'App',
  components:{
    Game,
    Header
  },

  data(){
    return {
      name:''
    }
  },
  created() {//Hook; chargement de l'application et remplie des données
  let name = prompt('Quel est votre nom');
  this.name = name;
  }
}
</script>

<template>
<Header :name="this.name"/> 
    <Game />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
#app {
  max-width: 360px;
}
body{
  background: azure;
}
</style>
