<template>
  <div id='app'>
    <win311-icon Nombre='msdos'></win311-icon>
  </div>
</template>

<script>
import Win311Icon from './components/Win311Icon.vue'
export default {
  name: 'App',
  components: {
    'win311-icon': Win311Icon
  }
}
</script>

<style>
body {
background: turquoise;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
