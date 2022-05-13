<template>
  <div id="app">
    <Header></Header>
    <Productos :productos="productos" :imgfavorito="imgfavorito" @agregar-al-carrito="AgregarProducto"></Productos>
    <Carrito :productoCarrito="productoCarrito" :cantidad="cantidad"></Carrito>
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
        cantidad: 0,
        imgfavorito: 'fav.png',
        productos:
        [
            {
              id: 1,
              url: 'hamburguesa-clasica.jpg',
              descripcion: 'Hamburguesa clasica',
              precio: 100,
              disponibilidad: true,
              favorito: true
            },
            {
              id: 2,
              url: 'hamburguesa-doble.jpg',
              descripcion: 'Hamburguesa doble',
              precio: 200,
              disponibilidad: true,
              favorito: false
            },
            {
              id: 3,
              url: 'hamburguesa-triple.jpg',
              descripcion: 'Hamburguesa triple',
              precio: 300,
              disponibilidad: false,
              favorito: false
            },
            {
              id: 4,
              url: 'hamburguesa-triple.jpg',
              descripcion: 'Hamburguesa triple',
              precio: 300,
              disponibilidad: true,
              favorito: false
            },
        ]
    }
  },
  methods:{
    // AgregarProducto(id){
    //   const resul = this.productos.find((prod) => prod.id == id);
    //   const carr = this.productoCarrito.find((prod) => prod.id == id);
    //   if (resul.id != carr?.id){
    //     this.cantidad++
    //     this.productoCarrito.push(resul)
    //   }
    //   else {
    //     this.productoCarrito.push(resul)
    //   }
    // }
    AgregarProducto(id){
      try{
        const res = this.productos.find((prod) => prod.id == id);
        const bag = this.productoCarrito.find((prod) => prod.id == id);
        console.log(res)
        console.log(bag)
        if (res.id != bag?.id)
          {
            this.cantidad++
            this.productoCarrito.push(res)
          }
          else
          {
            this.productoCarrito.push(res)
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
