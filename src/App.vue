<!-- Representa el html (Estructura) -->
<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="dark">
      <b-navbar-brand href="#">JADCS SOFTWARE</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item v-on:click="getResumen" v-if="is_auth">
            Resumen Usuario
          </b-nav-item>
          <b-nav-item v-on:click="agregar_doc" v-if="is_auth">
            Agregar Documento
          </b-nav-item>
          <b-nav-item v-on:click="logOut" v-if="is_auth">
            Cerrar sesión
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <div class="main-component">
      <b-container class="p-4 mt-5">
        <router-view v-on:log-in="logIn"></router-view>
      </b-container>
    </div>
  </div>
  <!--
  <div id="app">
    <div class="encabezado">
      <img id="logo" src="./assets/JADCSlogo.png" />
    </div>

    <table class="menu">
      <tr>
        <td class="botones">
          <button v-on:click="getResumen" v-if="is_auth">
            Resumen Usuario
          </button>
        </td>
        <td class="comp" rowspan="3">
          <div class="main-component">
            <router-view v-on:log-in="logIn"></router-view>
          </div>
        </td>
      </tr>
      <tr>
        <td class="botones">
          <button v-on:click="agregar_doc" v-if="is_auth">
            Agregar Documento
          </button>
        </td>
      </tr>
      <tr>
        <td class="botones">
          <button v-on:click="logOut" v-if="is_auth">Cerrar sesión</button>
        </td>
      </tr>
    </table>

    <div class="footer">
      <h2 class="h1">JADCS LTDA</h2>
    </div>
  </div>
  -->
</template>

<!-- Representa el js (Comportamiento) -->
<script>
export default {
  name: "App",
  components: {},
  data: function () {
    return {
      is_auth: localStorage.getItem("isAuth"),
    };
  },
  methods: {
    updateAuth: function () {
      var self = this;
      self.is_auth = localStorage.getItem("is_Auth") || false;
      if (self.is_auth == false) {
        self.$router.push({ name: "login" });
      } else {
        let username = localStorage.getItem("current_username");
        self.$router.push({ name: "sesionIn" });
      }
    },
    logIn: function (username) {
      localStorage.setItem("current_username", username);
      localStorage.setItem("is_Auth", true);
      this.updateAuth();
    },
    logOut: function () {
      localStorage.removeItem("is_Auth");
      localStorage.removeItem("current_username");
      this.updateAuth();
    },
    iniciar: function () {
      let auth = localStorage.getItem("is_Auth");
      let sesion = auth.localeCompare(false);
      if (sesion == 0) {
        if (this.$route.name != "login") {
          this.$router.push({ name: "login" });
        }
      } else {
        window.alert("Sesión ya iniciada");
      }
    },
    getResumen: function () {
      if (this.$route.name != "perfil") {
        let auth = localStorage.getItem("is_Auth");
        let sesion = auth.localeCompare(true);
        if (sesion == 0) {
          let theUsername = localStorage.getItem("current_username");
          this.$router.push({
            name: "perfil",
            params: { username: theUsername },
          });
        } else {
          window.alert("No ha iniciado sesión");
        }
      }
    },
    agregar_doc: function () {
      if (this.$route.name != "agregardoc") {
        let auth = localStorage.getItem("is_Auth");
        let sesion = auth.localeCompare(true);
        if (sesion == 0) {
          let username = localStorage.getItem("current_username");
          this.$router.push({ name: "agregardoc" });
        } else {
          window.alert("No ha iniciado sesión");
        }
      }
    },
  },
  created: function () {
    this.$router.push({ name: "root" });
    this.updateAuth();
  },
};
</script>

<!-- Representa el css (Estilo) -->
<style>
</style>
