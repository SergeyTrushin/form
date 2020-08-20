<template>
    <form @submit.prevent="submit">

        <h2>Новый клиент</h2>

        <div class="input">
            <input id="secondName" 
            	   type="text" 
                   v-model.trim="secondName"
                   :class="{invalid: ($v.secondName.$dirty && !$v.secondName.required)}"
                   required 
            >
            <label for="secondName">Фамилия*</label>

            <div v-if="$v.secondName.$dirty && !$v.secondName.required"
				   class="help-text" 
            >
            	Пожайлуста, введите вашу фамилию!
            </div>
        </div>

        <div class="input">
            <input id="firstName" type="text" required 
                   v-model.trim="firstName"
                   :class="{invalid: ($v.firstName.$dirty && !$v.firstName.required)}"
            >
            <label for="firstName">Имя*</label>

            <div v-if="$v.secondName.$dirty && !$v.secondName.required"
				   class="help-text" 
            >
            	Пожайлуста, введите ваше имя!
            </div>
        </div>

        <div class="input">	
            <input id="middleName" type="text" v-model.trim="middleName">
            <label for="middleName">Отчество</label>
        </div>

        <div class="input">
            <input type="text" id="date"
                   onfocus="this.type='date' " 
                   onblur= "this.type='text' "
                   v-model="date"
                   :class="{invalid: ($v.date.$dirty && !$v.date.required)}"
                   required
            />
            <label for="date">Дата рождения*</label>

            <div v-if="$v.date.$dirty && !$v.date.required"
				   class="help-text" 
            >
            	Пожайлуста, введите дату вашего рождения!
            </div>
        </div>

        <div class="input">
            <input id="phone" type="tel" required 
                   v-model.trim="phone"
                   :class="{invalid: ($v.phone.$dirty && !$v.phone.required) || ($v.phone.$dirty && !$v.phone.minLength) }"
                   required
                   
            >
            <label for="phone">Телефон*</label>

            <div v-if="$v.phone.$dirty && !$v.phone.required"
				   class="help-text" 
            >
            	Пожайлуста, введите ваш номер телефона!
            </div>

            <div v-if="$v.phone.$dirty && !$v.phone.minLength"
				   class="help-text" 
            >
            	Номер должен сожержать минимум 11 цифр и начинаться с +7
            </div>
        </div>

        <div class="input">
            <select name="gender" id="gender" v-model="gender">
                <option value="male">Мужской</option>
                <option value="female">Женский</option>
            </select>
            <label for="gender">Пол</label>
        </div>

        <div class="input">
            <select id="group"
            	    multiple 
            	    v-model="group" 
					:class="{invalid: ($v.group.$dirty && !$v.group.required)}"
            	    required>
                <option disabled class="selectHeader">Группа клиентов*</option>
                <option value="VIP">VIP</option>
                <option value="PROBLEM">Проблемные</option>
                <option value="OMS">ОМС</option>
            </select>
            
            <div v-if="$v.group.$dirty && !$v.group.required"
				   class="help-text" 
            >
            	Пожайлуста, выберите хотя бы одну группу клиетов!
            </div>
        </div>

        <div class="input">
            <select name="doc" id="doc" v-model="doc">
                <option value="IVANOV">Иванов</option>
                <option value="ZAHAROV">Захаров</option>
                <option value="CHERNICHEVA">Чернышева</option>
            </select>
            <label for="doc">Лечащий врач</label>
        </div>

        <input id="sms" type="checkbox" v-model="sms">
        <label for="sms">Не отправлять СМС</label>

        <button type="submit" @click="submit">
            Продолжить
        </button>
    </form>
</template>

<script>
import {required, minLength} from "vuelidate/lib/validators"

export default {
    data: ()=>({
    	secondName: "",
        firstName: "",
        middleName: "",
        date: "",
        phone: "+7",
        gender: "",
        group: [],
        doc: "",
        sms: true
    }),

    validations: {
        secondName: {
            required,
            minLength: minLength(2)
        },
        firstName: {
            required
        },
        date: {
            required,
        },
        phone: {
            required,
            minLength: minLength(12)
        },
        group: {
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

<style lang="scss">

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