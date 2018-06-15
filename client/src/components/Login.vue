<template>
    <v-layout>
      <v-flex>
        <panel title="Login">
          <v-text-field
              label="Email"
              v-model="email"
            ></v-text-field>
            <v-text-field
              type="password"
              label="Password"
              v-model="password"
            ></v-text-field>
          <div v-html="error" class="error" v-if="isError"></div>
          <v-btn
            color="info"
            @click="login">Login</v-btn>
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
      isError: false
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
        this.isError = false
      } catch (error) {
        this.error = error.response.data.error
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
