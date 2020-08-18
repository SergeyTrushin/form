<template>
  <div id="app">
      <MainAttributes/>
  </div>
</template>

<script>
import { required, minLength, between } from 'vuelidate/lib/validators'
import MainAttributes from "./components/MainAttributes"

export default {
  name: 'App',
  components: {
    MainAttributes,
  },
  data(){
    return{
      name: '',
      age: 0
    }
  },
   validations: {
    name: {
      required,
      minLength: minLength(4)
    },
  },
  methods:{
    submit(){
      alert(1)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-size: 18px;
  font-family: sans-serif;
}
</style>
