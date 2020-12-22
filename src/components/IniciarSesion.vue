<template>
  <div class="mt-5">
    <form v-on:submit.prevent="processAuthUser">
      <b-row md="5" class="justify-content-md-center">
        <b-col>
          <p class="h3">Nombre de usuario</p>
          <b-form-input type="text" v-model="user_in.idUsuario"> </b-form-input>
        </b-col>
      </b-row>
      <b-row md="5" class="justify-content-md-center">
        <b-col>
          <p class="h3">Contraseña</p>
          <b-form-input type="password" v-model="user_in.contrasenia">
          </b-form-input>
        </b-col>
      </b-row>
      <b-row class="justify-content-md-center mt-3">
        <b-col>
          <b-button variant="dark" type="submit" size="lg"
            >Iniciar Sesión</b-button
          >
        </b-col>
      </b-row>
    </form>
  </div>
</template>

<!--
  <div id="AuthUser" class="auth_user">
    <div class="container_auth_user">
      <div>
        <img src="./assets/JADCSlogo.png" />
      </div>

      <form v-on:submit.prevent="processAuthUser">
        <input type="text" v-model="user_in.idUsuario" placeholder="Usuario" />
        <br />
        <input
          type="password"
          v-model="user_in.contrasenia"
          placeholder="Contraseña"
        />
        <br />
        <button type="submit">Iniciar Sesión</button>
      </form>
    </div>
  </div>
-->

<script>
import axios from "axios";
export default {
  name: "login",
  data: function () {
    return {
      user_in: {
        idUsuario: "",
        contrasenia: "",
      },
    };
  },
  methods: {
    processAuthUser: function () {
      var self = this;
      axios
        .post(
          "https://jadcs-backend.herokuapp.com/usuario/autenticacion/",
          self.user_in,
          { headers: {} }
        )
        .then((result) => {
          alert("Autenticación Exitosa");
          self.$emit("log-in", self.user_in.idUsuario);
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