<template>
  <div class='icono' v-on:click="select($event)">
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
      console.log(this.title);
      document.querySelectorAll(`.${this.title}`).forEach(element => element.classList.toggle("selected"));
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
