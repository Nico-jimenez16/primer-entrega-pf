<template>
  <div id="app">
    <Header></Header>
    <Productos :productos="productos" :imgfavorito="imgfavorito" @agregar-al-carrito="AgregarProducto"></Productos>
    <Carrito :productoCarrito="productoCarrito" :cantidadcarrito="cantidadcarrito"></Carrito>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Productos from './components/Productos.vue'
import Carrito from './components/Carrito.vue'


export default {
  name: 'App',
  components: {
    Header,
    Productos,
    Carrito
  },
  data(){
    return {
        productoCarrito: [],
        cantidadcarrito: 0,
        imgfavorito: 'fav.png',
        productos:
        [
            {
              id: 1,
              url: 'hamburguesa-clasica.jpg',
              descripcion: 'Hamburguesa clasica',
              precio: 100,
              disponibilidad: true,
              favorito: true,
              enCarrito: 0
            },
            {
              id: 2,
              url: 'hamburguesa-doble.jpg',
              descripcion: 'Hamburguesa doble',
              precio: 200,
              disponibilidad: true,
              favorito: false,
              enCarrito: 0
            },
            {
              id: 3,
              url: 'hamburguesa-triple.jpg',
              descripcion: 'Hamburguesa triple',
              precio: 300,
              disponibilidad: false,
              favorito: false,
              enCarrito: 0
            },
            {
              id: 4,
              url: 'lomito.jpg',
              descripcion: 'Lomito Completo',
              precio: 800,
              disponibilidad: true,
              favorito: false,
              enCarrito: 0
            },
        ]
    }
  },
  methods:{
    AgregarProducto(id){
      try{
        const res = this.productos.find((prod) => prod.id == id);
        let bag = this.productoCarrito.find((prod) => prod.id == id);
          if (res.id == bag?.id)
            {
              res.enCarrito++
            }
            else
            {
              this.cantidadcarrito++
              this.productoCarrito.push(res)
              res.enCarrito++
            }
      }
      catch(err){
        console.error(err)
      }
    }
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
