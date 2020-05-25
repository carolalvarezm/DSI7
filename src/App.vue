<template>
  <div id='app'>
    <win311-icon Nombre='msdos' id="iconoexterior" @seleccionar="unselect"></win311-icon>
    <win311-window Tipo='cpanel' id="ventana1" @seleccionar="unselect"></win311-window>
    <win311-window Tipo='apps' id="ventana2" @seleccionar="unselect"></win311-window>
  </div>
</template>

<script>
import Win311Icon from "./components/Win311Icon.vue";
import Win311Window from "./components/Win311Window.vue";
export default {
  name: "App",
  components: {
    "win311-icon": Win311Icon,
    "win311-window": Win311Window
  },
  methods: {
    unselect: function (title) {
      alert(`Has seleccionado ${title}`);
    }
  }
};
</script>

<style>
body {
background: #079582;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#ventana1{
  position:relative;
  z-index:1;
  left:400px;
}
#ventana2{
  position:relative;
  z-index:1;
  left:500px;
  bottom:200px;
}
#iconoexterior{
  position:relative;
  left: 500px;
}
</style>
