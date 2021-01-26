<template>
  <v-form ref="form" v-model="valid" lazy-validation class="login" @submit.prevent="login">
    <v-text-field v-model="email" type="email" :rules="emailRules" label="E-mail" required></v-text-field>
    <v-text-field v-model="password" type="password" :rules="passwordRules" label="Password" required ></v-text-field>
    <v-btn color="primary" @click="submit" > Login </v-btn>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
    ],
    password: '',
    passwordRules: [
      v => !!v || 'password is required'
    ]
  }),

  methods: {
    login: function () {
      const email = this.email
      const password = this.password
      this.$store.dispatch('login', { email, password })
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err))
    }
  }
}
</script>
