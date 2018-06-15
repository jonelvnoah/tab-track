<template>
    <v-layout column>
      <v-flex>
        <panel title="Register">
          <v-text-field
            label="Email"
            v-model="email"
          ></v-text-field>
          <v-text-field
            type="password"
            label="Password"
            v-model="password"
          ></v-text-field>
         <br>
         <div v-if="isRegister" class="success">Register Success!</div>
         <div v-html="error" class="error" v-if="isError"></div>
         <v-btn
          color="info"
          @click="register">Register</v-btn>
        </panel>
      </v-flex>
    </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      email: '',
      password: '',
      error: null,
      isRegister: false,
      isError: true
    }
  },
  methods: {
    async register () {
      try {
        const res = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        console.log(res)
        this.$store.dispatch('setToken', res.data.token)
        this.$store.dispatch('setUser', res.data.user)
        this.isRegister = true
        this.isError = false
      } catch (error) {
        this.error = error.response.data.error
        this.isRegister = false
        this.isError = true
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
