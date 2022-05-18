<template>
  <div id="app">
    <Header :datos="datos"></Header>
    <Productos :datos="datos" :productos="productos" :imgfavorito="imgfavorito" @agregar-al-carrito="AgregarProducto" @delete-al-carrito="DeleteCarrito" ></Productos>
    <Carrito :datos="datos" :total="total" :productoCarrito="productoCarrito"></Carrito>
    <Login @resultado-del-login="MostrarDatos"></Login>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Productos from './components/Productos.vue'
import Carrito from './components/Carrito.vue'
import Login from './components/Login.vue'



export default {
  name: 'App',
  components: {
    Header,
    Productos,
    Carrito,
    Login
  },
  data(){
    return {
        productoCarrito: [],
        datos: false,
        total: 0,
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
      
    // AGREGAR PRODUCTO AL CARRITO , SI ESTA SOLO SUMA CANTIDAD Y PRECIO Y SI NO ESTA LO AGREGA

    AgregarProducto(id){
      try{

        let res = this.productos.find((prod) => prod.id == id);
        let bag = this.productoCarrito.find((prod) => prod.id == id);
          if (bag)
            {
              this.total = 0
              this.productoCarrito.map((producto) => {
                if(producto.id == bag.id)
                {
                  producto.enCarrito++
                  this.total += producto.enCarrito * producto.precio
                }
                else
                {
                  this.total += producto.enCarrito * producto.precio
                }
              });
              console.log('Existe en carrito')
            }
            else
            {
              this.productoCarrito.push(res)
              this.productoCarrito.map((producto) => {
                if(producto.id == res.id){
                  producto.enCarrito++
                  this.total += producto.enCarrito * producto.precio
                }
              });
              console.log('No existe en carrito')
            }
      }
      catch(err){
        console.error(err)
      }
    },

    // ELIMINA PRODUCTO DEL CARRITO , SI ESTA MAS DE 1 VES SOLO RESTA CANTIDAD Y PRECIO Y SI ES EL ULTIMO LO ELIMINA DEL ARRAY PRODUCTO EN CARRITO

    DeleteCarrito(id){
      try{

        let bag = this.productoCarrito.find((prod) => prod.id == id);
        if (bag){
          if(bag.enCarrito == 1)
            {
                bag.enCarrito--
                let pos = this.productoCarrito.indexOf(bag)
                this.productoCarrito.splice(pos , 1)
                this.total -= bag.precio
            }
          else
            {
              this.productoCarrito.map((producto) => {
                if(producto.id == bag.id)
                {
                  producto.enCarrito--
                  this.total -= producto.precio
                }
              });
            }
        }
      }

      catch(err){
        console.error(err)
      }
    },

    // FUNCION QUE PONE EL TRUE LA VARIBALE DATOS SI EL LOGIN FUE EXITOSO Y MUESTRA LOS COMPONENTE

    MostrarDatos(res){
      this.datos = res
      console.log('Llego bien hasta el Mostrar Datos del App.Vue')
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
