<template>
  <v-toolbar fixed class="red darken-2" dark>
    <v-toolbar-title class="mr-4">
     <span class="home" @click="navigateTo({name:'root'})"> SongTracker</span>
    </v-toolbar-title>

 
    <v-toolbar-items>
       <v-btn flat dark @click="navigateTo({name:'songs'})">
          Browse
        </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
       <v-btn flat dark @click="navigateTo({name:'login'})" v-if="!$store.state.isUserLoggedIn">
          Log In
        </v-btn>

        <v-btn flat dark @click="navigateTo({name:'register'})"
        v-if="!$store.state.isUserLoggedIn">
          Sign Up
        </v-btn>

        <v-btn flat dark @click="logout"
        v-if="$store.state.isUserLoggedIn">
          LogOut
        </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>

export default {
  methods:{
    navigateTo(route){
      this.$router.push(route);
    },
    logout(){
      this.$store.dispatch('setToken',null)
      this.$store.dispatch('setUser',null)
      //Todo:redirect ro homepage
      this.$router.push({
        name: 'root'
      })
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home{
  cursor: pointer;
}
.home:hover{
  color: #E9E;
}
</style>
