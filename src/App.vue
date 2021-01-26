<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition" width="40"
        />
        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>
      <div id="nav">
        <router-link to="/about">About</router-link>
        <span v-if="isLoggedIn"> | <a @click="logout">Logout</a></span>
      </div>
    </v-app-bar>

    <v-main>

    <v-container>
      <v-col md="6" offset-md="3" class="grey lighten-5">
        <v-row>
          <v-col md="6">
            <v-btn to="/login" block class="primary" elevation="2" text>
              <span class="mr-2">Login</span>
            </v-btn>
          </v-col>
          <v-col md="6">
            <v-btn to="/register" block class="primary" elevation="2" text>
              <span class="mr-2">Register</span>
              <v-icon>mdi-open-in-new</v-icon>
            </v-btn>
          </v-col>
        </v-row>
        <router-view/>
      </v-col>
    </v-container>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },
  data: () => ({
    //
  }),
  //
  computed: {
    isLoggedIn: function () { return this.$store.getters.isLoggedIn }
  },
  methods: {
    logout: function () {
      this.$store.dispatch('logout')
        .then(() => {
          this.$router.push('/login')
        })
    }
  },
  created: function () {
    this.$http.interceptors.response.use(undefined, function (err) {
      return new Promise(function (resolve, reject) {
        if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
          this.$store.dispatch('logout')
        }
        throw err
      })
    })
  }
}
</script>
