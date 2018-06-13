<template>
    <div>
       <h1>Register</h1>

       <input
         type="email"
         name="email"
         v-model="email"
         placeholder="email">
        <br>
        <input
          type="password"
          name="password"
          v-model="password"
          placeholder="password">
        <br>
        <div v-if="isRegister" class="success">Register Success!</div>
        <div v-html="error" class="error" v-if="isError"></div>
        <button
          @click="register"
          >Register</button>
    </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
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
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
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
  color:red;
}
</style>
