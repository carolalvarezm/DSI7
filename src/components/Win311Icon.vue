<template>
  <div class='icono'>
    <div class='imagen' v-html='image'></div>
    <p>{{title}}</p>
  </div>
</template>

<script>
export default {
  name: "Win311Icon",
  props: {
    Nombre: String
  },
  data () {
    return {
      image: `<img src='${require(`../assets/icons/${this.Nombre}.png`)}'/>`,
      title: this.Nombre
    };
  }
};
</script>

<style scoped>
.icono{
  margin-left:10px;
}
img{
  width:100px;
  height:100px;
}
p{
  margin-top:5px;
  text-align:center;
  text-transform: capitalize;
}
</style>
