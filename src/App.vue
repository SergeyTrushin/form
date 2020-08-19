<template>
  <div id="app">
      <MainAttributes :class="{ hide : !showMain}" @next="showMain=false;showAdress=true"/>
      <Adress :class="{ hide : !showAdress}" @next="showAdress=false;showPasport=true " @back="showAdress=false;showMain=true "/>
      <Pasport :class="{ hide : !showPasport}" @back="showPasport=false;showAdress=true "/>
  </div>
</template>

<script>
import MainAttributes from "./components/MainAttributes"
import Adress from "./components/Adress"
import Pasport from "./components/Pasport"

export default {
  name: 'App',
  components: {
    MainAttributes,
    Adress,
    Pasport
  },
  data(){
    return{
      showMain: true,
      showAdress: false,
      showPasport: false,
    }
  },
  methods:{
  }
}
</script>

<style lang="scss">
#app {
  font-size: 18px;
  font-family: sans-serif;
}

.hide{
  display: none;
}
</style>
