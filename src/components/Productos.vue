<template>
  <div class="Productos">
    <h1 class="text-3xl mt-4">{{ titulo }}</h1>
      <div class="text-black">
        <div class="w-full bg-state-300 p-4 movies mt-2">
            <div class="w-full flex flex-row flex-wrap justify-center">
                <div v-for="(producto, id) of productos" :key="id" class="relative shadow-lg hover:-translate-y-1 hover:scale-110 hover:bg-transparent duration-300 w-full xl:w-1/2 lg:w-1/3 xl:w-1/4 bg-transparent text-black font-bold m-4 border-2 rounded-xl p-4">
                    <img v-if="producto.favorito" :src="getImage(imgfavorito)" class="flex absolute top-0 right-0 w-1/3">
                    <div class="h-64">
                      <img :src="getImage(producto.url)" class="hover:skew-y-6 h-full m-auto" :alt="producto.descripcion">
                    </div>
                    <div class="flex flex-col w-full">
                        <div class="mt-2">
                            <p class="w-full">{{ producto.descripcion }}</p>
                            <p class="w-full">$ {{ producto.precio }}</p>
                        </div>
                    </div>
                    <div class="mt-2">
                      <button v-if="producto.disponibilidad" class="bg-lime-600 p-4 rounded-xl text-white" @click="AddCarrito(producto.id)">Agregar a Carrito</button>
                      <p v-else class="p-4 rounded-xl text-[#dc2626]">Sin Stock</p>
                      <p v-if="producto.enCarrito != 0" class="bg-red-600 w-1/6 rounded-xl text-white">{{producto.enCarrito}}</p>
                    </div>
                </div> 
            </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Productos',
  data(){
    return{
      titulo: 'Productos'
    }
  },
  props: {
    productos:{
      type: Array,
      required: true
    },
    imgfavorito:{
      type: String
    }
  },
  methods: {
    getImage(img){
      return require(`@/assets/images/${img}`)
    },
    AddCarrito(id){
      this.$emit("agregar-al-carrito" , id)
    }
  }
  
}
</script>