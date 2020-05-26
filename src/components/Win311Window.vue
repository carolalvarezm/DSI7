<template>
  <div class='ventana'>
    <div class="barra">
      <p class="icono-barra">-</p>
      <p>{{title}}</p>
      <p class="icono-barra">▼</p>
    </div>
    <div class="menu">
      <p>Settings</p>
      <p>Help</p>
    </div>
    <div class="iconos">
    <win311-icon v-for="u in iconos" :key="u" :Nombre="u" @alert="alert"></win311-icon>
    </div>
    <div class="ayuda">
      Select app to open...
    </div>
  </div>

</template>

<script>
import Win311Icon from "@/components/Win311Icon.vue";
import tipos from "@/assets/windows.json";
export default {
  name: "Win311Window",
  components: {
    "win311-icon": Win311Icon
  },
  props: {
    Tipo: String
  },
  data () {
    return {
      iconos: tipos[this.Tipo].icons,
      title: tipos[this.Tipo].title
    };
  },
  methods: {
    alert: function (title) {
      this.$emit("alert", title);
    }
  }

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="postcss">
.ventana{
  background:white;
  width:600px;
  height:400px;
}
.barra{
  background: #050362;
   height:35px;
  color:white;
  display:flex;
  justify-content:space-between;
  align-items:center;
  flex-direction:row;
}
.menu{
  background:white;
  color:gray;
  border-bottom:2px groove black;
  width:600px;
  height:25px;
  display:flex;
  justify-content:left;
  align-items:center;
  flex-direction:row;
  & p{
    margin-left:10px;
  }
}

.iconos{
  margin-top:10px;
  display:flex;
  flex-direction:row;
  flex-wrap:wrap;

}
.icono-barra{
  width: 35px;
  height:35px;
  font-size:20px;
  background-color:#b9b9b9;
}
.ayuda{
  width:600px;
  height:25px;
  background:#b9b9b9;
  position:absolute;
  bottom:0px;
  color:black;
  text-align:start;
}
</style>
