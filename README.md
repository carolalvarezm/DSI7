# Práctica 12: VueJS
## Instalando VueJS y creando la estructura del proyecto
* Lo primero que debemos hacer al trabajar con Vue es instalarlo para ello hacemos:
    ```bash
        $npm install -g @vue/cli
        $vue --version
    ```
![Vue-version](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vue-version.png)
* Después hacemos un *vue create* para crear la estructura del proyecto:
    ```bash
     $vue create dsi-p6-win311
    ```
![Vue create](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vue_create.png)
![Estructura](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vuejs_create2.png)

* Después de eso ya tenemos creada la estructura del proyecto.
* Para desplegar la aplicación en local utilizamos:
```bash
$npm run serve
```
![npm run serve](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vue_serve.png)

## App.vue
* A continuación tenemos el App.vue que será nuestro componente principal de la aplicación:
### template
* Primero tenemos la parte de plantillas donde ponemos la estructura que tendrá nuestra aplicación. En este caso contiene un icono y dos ventanas llamando a los componentes que he creado:
```vue
<template>
  <div id='app'>
    <win311-icon Nombre='msdos' id="iconoexterior"></win311-icon>
    <win311-window Tipo='cpanel' id="ventana1"></win311-window>
    <win311-window Tipo='apps' id="ventana2"></win311-window>
  </div>
</template>
```
### script
* Después tenemos la parte de los scripts donde importaremos los componentes que vamos a utilizar en la parte de template:
```vue
    <script>
    import Win311Icon from "./components/Win311Icon.vue";
    import Win311Window from "./components/Win311Window.vue";
    export default {
    name: "App",
    components: {
        "win311-icon": Win311Icon,
        "win311-window": Win311Window
    },
    };
    </script>
```
### style
* Por último tenemos los estilos, es este caso le he añadido un fondo turquesa al fondo y fijado la posición de las ventanas y el icono:
```vue
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

```
## Componentes
* Lo que tenemos a continuación son los componentes de ventana (Win311Window) e icono (Win311Icon):

### Win311Icon
### template
* Para los iconos utilizaremos un div en el que se incluirá una imagen con código html desde los scripts y un texto que contendrá el título del icono que le daremos a través de un prop "Nombre" desde el elemento padre que lo utilizemos.
```vue
<template>
  <div class='icono'>
    <div class='imagen' v-html='image'></div>
    <span :class="title">{{title}}</span>
  </div>
</template>

```
### script
* En la parte de los scripts lo primero que hacemos es darle un nombre e incluir en los *props* Nombre como dijimos antes.
* Después le damos valor a image que incluirá el html de una imagen del mismo nombre que el que le pasamos a la etiqueta y un título.
```vue
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
```
### style
* Finalmente tenemos los estilos, que se centran en centrar los iconos, fijar un tamaño para las imágenes y alinear el texto.
```vue
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
</style>

```
### Win311Window
* Una vez que tenemos los iconos nos centramos en las ventanas, he definido un json que especifica que iconos lleva cada ventana y su título:
```json
{
    "apps": {
        "title": "Aplicaciones",
        "icons": ["paintbrush", "calc", "write", "notepad", "clock"]
    },
    "cpanel": {
        "title": "Panel de Control",
        "icons": ["calendar", "charmap", "clipboard", "colors", "desktop", "keyboard", "cd", "fonts", "international", "programs"]
    }
}
```
### template
* La plantilla para la ventana sería la siguiente:
```vue
<template>
  <div class='ventana'>
    <div class="barra">
      <p class="icono-barra">-</p>
      <p>{{titulo}}</p>
      <p class="icono-barra">▼</p>
    </div>
    <div class="menu">
      <p>Settings</p>
      <p>Help</p>
    </div>
    <div class="iconos">
    <win311-icon v-for="u in iconos" :key="u" :Nombre="u"></win311-icon>
    </div>
    <div class="ayuda">
      Select app to open...
    </div>
  </div>

</template>
```
* Contiene una barra que contendrá el título, un menú con las opciones settings y help, la colección de iconos y en la parte inferior un mensaje *Select app to open...*.
* Lo más interesente sería la colección de iconos en la que utilizo una etiqueta win311-icon de nuestro componente y en la que se utiliza un *v-for* para que haya tantos como los que hemos definido en el json para ese tipo de ventana.
### script
* En la parte de los scripts lo primero que hacemos es importar el componente que creamos para los iconos y el json con las definiciones de las ventanas.
* Podemos ver que también se incluye un prop *Tipo* que utilizaremos para designar el tipo de ventana.
* Por último en data devolvemos la colección de iconos y el título de la ventana que hemos recogido del json.
```vue
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
      titulo: tipos[this.Tipo].title
    };
  }
};
</script>
```
### style
* Los estilos que he definido para las ventanas son los siguientes:
```vue
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
```
![Resultado final](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/resultado.png)
## Desplegando en Github pages
* Para desplegar nuestra aplicación en GHpages lo que hacemos es crear un nuevo fichero de configuración *vue.config.js* en el que cambiaremos el *publicpath* para que sea el del repositorio de la práctica:
```javascript
module.exports = {
    publicPath: process.env.NODE_ENV === 'production' ? '/dsi-p6-win311-alu0100944723/' : '/'
}
```
* Después de esto para crear los archivos de producción ejecutamos:
```bash
$npm run build
```
* Para subirlo utilizamos otro script de npm *deploy* que contiene ```npx gh-pages -d dist```
```bash
$npm run deploy
```

![npm run build](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vue_build.png)
![npm run deploy](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/vue-deploy.png)
## Retos
### Reto 1: Seleccionar elementos.
* Para seleccionar los elementos lo primero que hice fue añadir un evento *click* a la parte de template de mi componente Win311Icon:
```vue
<template>
  <div class='icono' @click="select($event)">
    <div class='imagen' v-html='image'></div>
    <span :class="title">{{title}}</span>
  </div>
</template>
```
* También añadí el método select que añadirá la clase *selected* al span con ese title.
```vue
  <script>
  exports default{
  ...,
  methods: {
      select: function (event) {
        document.querySelector(`.${this.title}`).classList.toggle("selected");
      }
  };
  }
  </script>
```
* Finalmente añadí un estilo para que remarcara en azul si se tenía esa clase:
```vue
<style>
.selected{
    background:blue;
    color:white;
  }
</style>
```
![Reto 1](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/reto1.gif)
### Reto 2: Deseleccionar el resto cuando se selecciona uno.
* Para este reto el primer cambio está en añadir al método *select* de Win311Icon un this.emit para que comunique al padre que ha sido seleccionado.
* También añadimos otro método *unselect* que eliminará la clase *selected* del texto.
```vue
#Win311Icon.vue
  <script>
  exports default{
  ...,
  methods: {
      select: function (event) {
        document.querySelector(`.${this.title}`).classList.toggle("selected");
        this.$emit("selected", this.title);
      },
      unselect: function () {
      document.querySelector(`.${this.title}`).classList.remove("selected");
    }
  };
  }
  </script>
```
* A continuación añadí un manejador de evento *selected* en los iconos de App.vue y Win311Window.vue, en las ventanas de App.vue incluimos otro para *unselect*:
```vue
#Win311Window.vue
<template>
...
<win311-icon v-for="u in iconos" :key="u" :Nombre="u" @selected="selected"></win311-icon>
...
</template>
```

```vue
#App.vue
<template>
...
<win311-icon Nombre='msdos' id="iconoexterior" @alert="alert" @selected="unselect"></win311-icon>
<win311-window Tipo='cpanel' id="ventana1" @alert="alert" @unselect="unselect"></win311-window>
<win311-window Tipo='apps' id="ventana2" @alert="alert" @unselect="unselect"></win311-window>
...
</template>
```
* A continuación añadí a Win311Window un método *selected* que emitirá un evento *unselect*.
* También añdí otro llamado *unselect* que llamará al método *unselect* de sus iconos hijo excepto el que ha sido seleccionado.
```vue
#Win311Window.vue
  <script>
  exports default{
  ...,
  methods: {
    selected: function (title) {
      this.$emit("unselect", title);
    },
    unselect: function (title) {
      this.$children.forEach(element => {
        if (title !== element.title) {
          element.unselect();
        }
      });
    }
  };
  }
  </script>
```
* Finalmente añadimos un método a App.vue que llamará al unselect de cada uno de sus hijos excepto el que ha sido seleccionado:
```vue
#App.vue
  <script>
  exports default{
  ...,
   methods: {
    unselect: function (title) {
      this.$children.forEach(element => {
        if (element.title !== title) {
          element.unselect(title);
        }
      });
    } 
  }
};
  </script>
```
  

![Reto 2](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/reto2.gif)
### Reto 3: Alerta al hacer doble click
* Para este reto lo primero que hacemos es incluir un manejador de eventos para el doble click en Win311Icon:
```vue
#Win311Icon.vue
<template>
...
<div class='icono' @click="select($event)" @dblclick="alert($event)">
...
</template>
```
* Añadimos también como antes un manejador para el custom event *alert* en los iconos de las ventanas y la app:
```vue
#Win311Window.vue
<template>
...
<win311-icon v-for="u in iconos" :key="u" :Nombre="u" @alert="alert" @selected="selected"></win311-icon>
...
</template>
```
```vue
#App.vue
<template>
...
  <win311-icon Nombre='msdos' id="iconoexterior" @alert="alert" @selected="unselect"></win311-icon>
  <win311-window Tipo='cpanel' id="ventana1" @alert="alert" @unselect="unselect"></win311-window>
  <win311-window Tipo='apps' id="ventana2" @alert="alert" @unselect="unselect"></win311-window>
...
</template>
```
* En el componente de Win311WIndow emitimos el evento alert cuando nos llega de un icono:
```vue
#Win311Window.vue
  <script>
  exports default{
  ...,
   methods: {
    alert: function (title) {
      this.$emit("alert", title);
    },
    } 
  }
};
  </script>
```
* Finalmente en App.vue cuando nos llega un evento emitimos una alerta:
```vue
#Win311Window.vue
  <script>
  exports default{
  ...,
   methods: {
    alert: function (title) {
      alert(`Has seleccionado ${title}`);
    },
    } 
  }
};
  </script>
```
![Reto 3](https://github.com/ULL-ESIT-DSI-1920/dsi-p6-win311-alu0100944723/blob/master/src/assets/Capturas_README/reto3.gif)