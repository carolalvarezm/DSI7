<template>
  <div class='icono' @click="select($event)">
    <div class='imagen' v-html='image'></div>
    <span :class="title">{{title}}</span>
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
  },
  methods: {
    select: function (event) {
      document.querySelector(`.${this.title}`).classList.toggle("selected");
      this.$emit("seleccionado", this.title);
      this.$emit("seleccionar", this.title);
    }
  }
};
</script>

<style scoped lang="postcss">
.icono{
  margin-left:10px;
}
img{
  width:100px;
  height:100px;
}
span{
  margin-top:5px;
  text-align:center;
  text-transform: capitalize;
}
.selected{
    background:blue;
  }
</style>
