<template>
  <form @submit.prevent>

    <h2>Документ</h2>

  	<div class="input">
            <select  id="document"
                     v-model="document"
                     :class="{invalid: ($v.document.$dirty && !$v.document.required)}" 
                     required>
                <option value="pasport">Паспорт</option>
                <option value="birth ">Свидетельство о рождении</option>
                <option value="driveLicense">Вод. удостоверени</option>
            </select>
            <label for="document">Тип документа</label>

            <div v-if="$v.document.$dirty && !$v.document.required"
              class="help-text" 
            >
              Пожайлуста, выберите тип документа!
          </div>
    </div>

    <div class="input">
          <input id="series" type="text" 
                  
          >
          <label for="series">Серия</label>
    </div>

    <div class="input">
          <input id="number" type="text" 
                  
          >
          <label for="number">Номер </label>
    </div>

    <div class="input">
          <input id="city" type="text" 
                  
          >
          <label for="city">Кем выдан </label>
    </div>

     <div class="input">
          <input type="text" id="date" name="date" 
                 onfocus="this.type='date' " 
                 onblur= "this.type='text' "
                 v-model="date"
                 :class="{invalid: ($v.date.$dirty && !$v.date.required)}" 
                 required 
          />
          <label for="date">Дата выдачи </label>
           <div v-if="$v.date.$dirty && !$v.date.required"
              class="help-text" 
            >
              Пожайлуста, введите дату выдачи документа!
          </div>
    </div>

    <button @click="submit">Готово</button>
    
    <button @click="$emit('back')">Назад</button>
  </form>
</template>

<script>
import {required} from "vuelidate/lib/validators"

export default{
  data: ()=>({
    document: "",
    date: ""
  }),
  validations: {
    document: {
      required
    },
    date: {
      required
    }
  },
  methods:{
        submit(){
            if (this.$v.$invalid){
                this.$v.$touch()
                return
            }
            this.$emit("success")
            
        },
    }

}

</script>