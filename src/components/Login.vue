<template>
    <div v-show="this.resultadoLogin == false">
        <div class="w-1/2 h-1/2 bg-lime-300 p-8 flex flex-col mt-12 mx-auto">
            <div class="h-auto">
                <h2 class="text-2xl text-black">Login</h2>
                <div class="flex justify-center w-full mb-2">
                    <input class="w-2/3 border p-4" type="text" placeholder="Ingrese usuario" v-model="usuario.nombre">
                    <!-- <p>{{usuario}}</p> -->
                </div>
                <div class="flex justify-center w-full">
                    <input class="w-2/3 border p-4" type="password" placeholder="Ingrese password" v-model.number="usuario.password">
                    <!-- <p>{{password}}</p> -->
                </div>
                    <!-- <p class="text-black mt-2">Registrarse</p> -->
                    <button class="w-2/3 p-2 border-2 mt-2 m-auto text-black" @click="ValidarLogin()">Ingresar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Login',
    data() {
        return {
            resultadoLogin: false,
            usuario:
            [
                {
                    nombre: '',
                    password: ''
                }
            ],
            usuarios:
            [
                {
                    nombre: 'Nicolas',
                    password: 12345
                },
                {
                    nombre: 'Felipe',
                    password: 123456
                }
            ]
        }
    },
    props:{

    },
    methods:{

        // FUNCION QUE VALIDA SI LOS DATOS INGRESADOS POR EL USUARIO SON CORRECTOS Y PONE EL TRUE LA VARIBALE "resultadoLogin" PARA SER ENVIADA AL COMPONENTE APP.VUE

        ValidarLogin(){
            const resultado = this.usuarios.filter((usuario) => this.usuario.nombre == usuario.nombre && this.usuario.password == usuario.password)
            console.log(resultado)
            if(resultado.length != 0) {
                this.resultadoLogin = true
                this.$emit("resultado-del-login" , this.resultadoLogin)
                alert('Login Exitoso')
            }
            else {
                alert('Login Fallido')
                this.$emit("resultado-del-login" , this.resultadoLogin)
            }
        }
    }
}
</script>

<style>

</style>"