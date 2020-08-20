<template>
  <div id="app">
      <MainAttributes :class="{ hide : !showMain}" @next="showMain=false;showAdress=true"/>
      <Adress :class="{ hide : !showAdress}" @next="showAdress=false;showPasport=true " @back="showAdress=false;showMain=true "/>
      <Pasport :class="{ hide : !showPasport}" @back="showPasport=false;showAdress=true" @success="openModal"/>

      <Modal v-if="showModal" @closeModal="closeModal"/>
  </div>
</template>

<script>
import MainAttributes from "./components/MainAttributes"
import Adress from "./components/Adress"
import Pasport from "./components/Pasport"
import Modal from "./components/Modal"

export default {
  name: 'App',
  components: {
    MainAttributes,
    Adress,
    Pasport,
    Modal
  },
  data(){
    return{
      showMain: true,
      showAdress: false,
      showPasport: false,
      showModal: false
    }
  },
  methods:{
    openModal(){
      this.showModal = true
    },
    closeModal(){
      this.showMain = true
      this.showModal = false
      this.showAdress = false
      this.showPasport = false
    }
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
