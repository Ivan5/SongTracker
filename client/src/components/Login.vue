<template>
<v-layout colum>
  <v-flex xs6 offset-xs3>
    <panel title="Login">
        <v-text-field 
          name="email"
          type="email"
          label="Email"
          v-model="email"></v-text-field>
        
        <v-text-field 
          name="password"
          type="password"
          label="Password"
          v-model="password"></v-text-field>

        <div class="error" v-html="error"></div><br>
        <v-btn class="red darken-2" dark @click="login">Login</v-btn>
    </panel>
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
      error:null
    }
  },
  methods:{
    async login () {
      try {
      const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
       })
       this.$store.dispatch('setToken',response.data.token)
       this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error{
  color:red;
}
</style>
