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

form{
    position: absolute;
    top: 50%;
    left: 50%;
    width: 500px;
    transform: translate(-50%,-50%);
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 1rem;
    button{
        border: none;
        outline: none;
        padding: 10px 0;
        cursor: pointer;
        background: #f7497d;
        color: #fff;
        text-transform: uppercase;
        width: 100%;
        margin-top: 15px;
    }

    @media(max-width: 768px){
      &{
        width: 100%;
        font-size: 13px;
        padding: 10px;
        h2{
          font-size: 15px;
        }
        .input{
          font-size: 13px;

        }
      }
    }
}

.input{
    position: relative;
    width: 100%;
    input,select{
        font-size: 18px;
        width: 100%;
        padding: 10px 0;
        margin: 0 0 18px 0;
        border: none;
        border-bottom: 2px solid #999;
        outline: none;
        &:focus ~label,
        &:valid ~label
        {
            top: -12px;
            left: 0;
            color: #000;
            font-size: 15px;
            font-weight: bold;
        }
    }

    .help-text{
      color: red;
      margin-bottom: 1rem;
    }

    .invalid{
        border-bottom: 2px solid #f7497d;
    }
    label{
        position: absolute;
        left: 0;
        top: 10px;
        color: #999;
        transition: .5s;
    }

}

#group{
    overflow: hidden;
}

.selectHeader{
    color: #000;
    font-size: 15px;
    font-weight: bold;
}
</style>
