<template>
  <v-container>
    <v-form>
      <v-text-field
        outline
        label=" E-Mail"
        :error-messages="errors"
        type="text"
        v-model="$v.email.$model"
      ></v-text-field>
      <v-text-field
        outline
        hide-details
        label="Password"
        type="password"
        v-model="password"
      ></v-text-field>
    </v-form>
    <v-btn color="primary" @click="login"> Login </v-btn>
  </v-container>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { validationMixin } from 'vuelidate';
import { required, minLength } from 'vuelidate/lib/validators';
export default {
  name: 'HelloWorld',

  data: () => ({
    email: '',
    password: '',
    errors:[]
  }),

  validations: {
    email: {
      required,
      minLength: minLength(6),
    },
  },
  methods: {
    login() {
      this.errors = []
      !this.$v.email.minLength &&
      this.errors.push('Name must be at most 6 characters long');
      !this.$v.email.required && this.errors.push('Email is required.');
      if( this.errors.length === 0 ){
        this.$router.push({name: 'products'})
      }

    }
  },
};
</script>

<style lang="scss">
.v-btn {
  color: red !important;

  margin-top: 10px;
}
.v-form {
  max-width: 50%;
  margin: 0 auto;
}
.v-btn .v-card {
  border-radius: 4px;
}
.v-card__title {
  text-transform: uppercase;
}
</style>
