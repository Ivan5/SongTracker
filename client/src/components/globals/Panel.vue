<template>
 <div class="white elevation-2">
      <v-toolbar flat dense class="red darken-2" dark>
        <vtoolbar-title>{{title}}</vtoolbar-title>
        <slot name="action" />
      </v-toolbar>
      

      <div class="pl-4 pr-4 pt-2 pb-2">
        <slot>
          No slot content defined
        </slot>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello World'
    }
  },
  props:[
    'title'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
