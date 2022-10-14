<template>
  <v-container>
    <v-form>
      <v-text-field
        outline
        label=" E-Mail"
        :error-messages="emailErrors"
        type="text"
        v-model="$v.email.$model"
      ></v-text-field>
      <v-text-field
        outline
        hide-details
        label="Password"
        type="password"
        v-model="$v.password.$model"
        :error-messages="passwordErrors"
      ></v-text-field>
    </v-form>
    <v-btn
      color="primary"
      @click="login"
    >
      Login
    </v-btn>
  </v-container>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { validationMixin } from 'vuelidate';
import { email, required, minLength } from 'vuelidate/lib/validators';
export default {
  name: 'HelloWorld',

  data: () => ({
    email: '',
    password: '',
    emailErrors: [],
    passwordErrors: [],
  }),

  validations: {
    password: {
      required,
      minLength: minLength(6),
    },
    email: {
      required,
      email,
    },
  },
  methods: {
    login() {
      this.passwordErrors = [];
      this.emailErrors = [];
      !this.$v.password.minLength &&
        this.passwordErrors.push('Password must be at most 6 characters long');
      !this.$v.password.required &&
        this.passwordErrors.push('password is required.');
      !this.$v.email.required && this.emailErrors.push('email is required.');
      !this.$v.email.email && this.emailErrors.push('email is incorrect.');
      if (this.emailErrors.length === 0 && this.passwordErrors.length === 0) {
        this.$router.push({ name: 'products' });
      }
    },
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
