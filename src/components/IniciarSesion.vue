<template>
    <div id="AuthUser" class="auth_user">
        <div class="container_auth_user">
            <h2>Autenticarse</h2>
            <form v-on:submit.prevent="processAuthUser" >
                <input type="text"
                    v-model="user_in.idUsuario"
                    placeholder="Usuario">
                <br>
                <input type="password"
                    v-model="user_in.contrasenia"
                    placeholder="Contraseña">
                <br>
                <button type="submit">Iniciar Sesión</button>
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "login",
    data: function(){
        return {
            user_in: {
                idUsuario:"",
                contrasenia:""
            }
        }
    },
  methods: {
    processAuthUser: function(){
            var self = this
            axios.post("http://127.0.0.1:8000/usuario/autenticacion/", self.user_in,  {headers: {}})
                .then((result) => {
                    alert("Autenticación Exitosa");
                    self.$emit('log-in', self.user_in.idUsuario)
                })
                .catch((error) => {
                    
                    if (error.response.status == "404")
                        alert("ERROR 404: Usuario no encontrado.");
                    
                    if (error.response.status == "403")
                        alert("ERROR 403: Contraseña Erronea.");  
                });
        },
  },
};
</script>

<style>
</style>