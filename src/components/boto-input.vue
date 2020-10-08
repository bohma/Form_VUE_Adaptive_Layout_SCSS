<template>
  <form id="form" class="form" @click.prevent="checkForm">
    <div class="inputs">
      <div class="inputs__input">
        <input
          id="company"
          class="inputs__input-item"
          placeholder="Ваше имя"
          :class="$v.form.company.$error ? 'is-invalid' : ''"
          v-model.trim="$v.form.company.$model"
        />
        <p
          v-if="$v.form.company.$dirty && !$v.form.company.required"
          class="invalid-feedback"
        >
          *Обязательное поле
        </p>
        <p
          v-if="$v.form.company.$dirty && !$v.form.company.minLength"
          class="invalid-feedback"
        >
          *Введите больше одного символа
        </p>
      </div>
      <div class="inputs__input">
        <input
          id="email"
          type="email"
          class="inputs__input-item"
          placeholder="Email"
          :class="$v.form.email.$error ? 'is-invalid' : ''"
          v-model.trim="$v.form.email.$model"
        />
        <p
          v-if="$v.form.email.$dirty && !$v.form.email.required"
          class="invalid-feedback"
        >
          *Обязательное поле
        </p>
        <p
          v-if="$v.form.email.$dirty && !$v.form.email.email"
          class="invalid-feedback"
        >
          *Введите корректно Email
        </p>
      </div>
      <div class="inputs__input">
        <input
          v-mask="'+38 (0##) ###-##-##'"
          id="tel"
          class="inputs__input-item"
          placeholder="Номер телефона"
          :class="$v.form.tel.$error ? 'is-invalid' : ''"
          v-model.trim="$v.form.tel.$model"
        />
        <p
          v-if="$v.form.tel.$dirty && !$v.form.tel.required"
          class="invalid-feedback"
        >
          *Обязательное поле
        </p>
        <p
          v-if="$v.form.tel.$dirty && !$v.form.tel.minLength"
          class="invalid-feedback"
        >
          *Введите корректно номер
        </p>
      </div>
    </div>
    <button type="submit" class="btn">Попробовать бесплатно</button>
  </form>
</template>

<script>
import { validationMixin } from "vuelidate";
import axios from "axios";
import {
  required,
  minLength,
  email,
  maxLength,
} from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],
  data() {
    return {
      chatId: "-402256735",
      token: "1175499824:AAH4B34VTAFZgEjM2toceA9wtubGH1wrCrI",
      form: {
        company: "",
        email: "",
        tel: "",
      },
      toSend: "",
    };
  },
  validations: {
    form: {
      company: { required, minLength: minLength(2) },
      email: { required, email },
      tel: { required, minLength: minLength(19), maxLength: maxLength(19) },
    },
  },
  methods: {
    checkForm() {
      this.$v.form.$touch();
      if (!this.$v.form.$error) {
        alert("Ваша заявка оставлена!");
        this.toSend = `name: ${this.form.company}%0Atel: ${this.form.email}%0Acountry: ${this.form.tel}%0A`;

        axios({
          method: "post",
                  url: `https://api.telegram.org/bot${this.token}/sendMessage?chat_id=${this.chatId}&text=${this.toSend}`,

          data: {},
        });

        this.form.company = "";
        this.form.email = "";
        this.form.tel = "";
      }
    },
  },
};
</script>

<style lang="scss" >
.inputs {
  display: flex;
  flex-wrap: wrap;
  &__input {
    position: relative;
    margin-bottom: 50px;
    padding-right: 24px;
    &-item {
      border: none;
      width: 260px;
      height: 55px;
      border-radius: 5px;
      padding-left: 18px;
      &:focus {
        outline: none;
      }
      &::placeholder {
        font-family: "Gilroy", sans-serif;
        font-size: 16px;
      }
    }
    & p {
      position: absolute;
      margin-top: 2px;
      font-size: 14px;
      color: rgb(255, 21, 21);
    }
  }
}
.btn {
  width: 330px;
  height: 55px;
  border-radius: 5px;
  border: none;
  background: #001515;
  color: #ffffff;
  font-family: "Gilroy", sans-serif;
  font-size: 18px;
  font-weight: 500;
  cursor: pointer;
  transition: 0.4s;

  &:focus {
    outline: none;
  }
  &:hover {
    background: #3b69ff;
    color: #ffffff;
  }
}
.is-invalid {
  border: 1px red solid;
}

@media screen and (max-width: 1023px) {
  .inputs {
    &__input {
      margin-bottom: 30px;
      &-item {
      }
    }
  }
}
@media screen and (max-width: 767px) {
  .inputs {
    display: block;
    &__input {
      margin-bottom: 24px;
      padding-right: 0;
      &-item {
        width: 100%;
      }
    }
  }
  .btn:hover {
    background: #001515;
    color: #ffffff;
  }
}
</style>
