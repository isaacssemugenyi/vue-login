<template>
    <v-form ref="form" v-model="valid" lazy-validation class="login" @submit.prevent="register">
        <v-text-field v-model="name" type="text" :rules="nameRules" label="Name" required autofocus></v-text-field>
        <v-text-field v-model="email" type="email" :rules="emailRules" label="E-mail Address" required></v-text-field>
        <v-text-field v-model="password" type="password" :rules="passwordRules" label="Password" required ></v-text-field>
        <v-text-field v-model="password_confirmation" type="password" :rules="passwordRules" label="Confirm Password" required ></v-text-field>
        <v-btn color="primary" @click="submit" > Register </v-btn>
    </v-form>
</template>

<script>
export default {
  data () {
    return {
      name: '',
      email: '',
      password: '',
      password_confirmation: '',
      is_admin: null
    }
  },
  methods: {
    register: function () {
      const data = {
        name: this.name,
        email: this.email,
        password: this.password,
        is_admin: this.is_admin
      }
      this.$store.dispatch('register', data)
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err))
    }
  }
}
</script>
