<template>
    <v-layout>
      <v-flex>
       <div class="white elevation-2">
         <v-toolbar class="cyan" dark flat dense>
           <v-toolbar-title>Login</v-toolbar-title>
         </v-toolbar>

         <div class="pl-4 pr-4 pt-2 pb-2">
          <v-text-field
            label="Email"
            v-model="email"
          ></v-text-field>
          <v-text-field
            type="password"
            label="Password"
            v-model="password"
          ></v-text-field>
         </div>
         <br>
         <div v-html="error" class="error"></div>
         <v-btn
          color="info"
          @click="login">Login</v-btn>
       </div>
      </v-flex>
    </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async login () {
      try {
        const res = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', res.data.token)
        this.$store.dispatch('setUser', res.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<style>
.error,
.success {
  color:white;
}
</style>
