<template>
  <form @submit.prevent>
  	<h2>Адрес</h2>

    <div class="input">
          <input id="index" type="text" 
                  
          >
          <label for="index">Индекс</label>
    </div>

    <div class="input">
          <input id="country" type="text" 
                  
          >
          <label for="country">Страна</label>
    </div>

    <div class="input">
          <input id="region" type="text" 
                  
          >
          <label for="region">Область</label>
    </div>

    <div class="input">
          <input id="city" type="text" 
                 required
                 v-model="city"
                 :class="{invalid: ($v.city.$dirty && !$v.city.required)}" 
                      
          >
          <label for="city">Город*</label>

          <div v-if="$v.city.$dirty && !$v.city.required"
           class="help-text" 
            >
              Пожайлуста, введите город вашего проживания!
          </div>
    </div>

    <div class="input">
          <input id="street" type="text" 
                  
          >
          <label for="street">Улица</label>
    </div>

    <div class="input">
          <input id="house" type="text" 
                  
          >
          <label for="house">Дом</label>
    </div>

    <button @click="submit">Продолжить</button>
    <button @click="$emit('back')">Назад</button>
  </form>
</template>

<script>
import {required} from "vuelidate/lib/validators"

export default{
  data: ()=>({
    city: ""
  }),
  validations: {
    city: {
      required
    }
  },
  methods:{
        submit(){
            if (this.$v.$invalid){
                this.$v.$touch()
                return
            }
            this.$emit('next')
        },
    }

}

</script>