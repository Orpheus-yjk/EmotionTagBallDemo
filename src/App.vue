<template>
  <div id="app">
    <CircleView/>
  </div>
</template>

<script>
import CircleView from './components/circleView.vue'

export default {
  name: 'App',
  components: { 
    CircleView,
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
