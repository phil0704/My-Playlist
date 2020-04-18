<template>
  <div id="app">
    <Vueplaylist />
  </div>
</template>

<script>
import Vueplaylist from './components/Vueplaylist.vue'


export default {
  name: 'App',
  components: {
   Vueplaylist
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>