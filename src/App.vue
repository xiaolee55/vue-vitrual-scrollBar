<template>
  <div id="app">
    <scrollBar/>
  </div>
</template>

<script>
import scrollBar from './core.vue'

export default {
  components: {
    scrollBar
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
}
</style>
