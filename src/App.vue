<!-- Representa el html (Estructura) -->
<template>
  <div id="app">
    <div class="encabezado">
      <img id="logo" src="./assets/JADCSlogo.png" />
    </div>

    <table class="menu">
      <tr>
        <td class="botones">
          <button v-on:click="getResumen" v-if="is_auth">Resumen Usuario</button>
        </td>
        <td class="comp" rowspan="3">
          <div class="main-component">
            <router-view  v-on:log-in="logIn" ></router-view> 
          </div>
        </td>
      </tr>
      <tr>
        <td class="botones">
          <button v-on:click="agregar_doc" v-if="is_auth">Agregar Documento</button>
        </td>
      </tr>
      <tr>
        <td class="botones">
          <button v-on:click="logOut" v-if="is_auth">Cerrar sesión</button>
        </td>
      </tr>      
    </table>

    <div class="footer">
      <h2>JADCS LTDA</h2>
    </div>
  </div>
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
    updateAuth: function(){
      var self = this
      self.is_auth  = localStorage.getItem('is_Auth') || false
      if(self.is_auth == false){
        self.$router.push({name: "login"})
      }else{
        let username = localStorage.getItem("current_username")
        self.$router.push({name: "sesionIn"})
      }  
    },
    logIn: function(username){

      localStorage.setItem('current_username', username)
      localStorage.setItem('is_Auth', true)
      this.updateAuth()
    },
    logOut: function(){
      localStorage.removeItem('is_Auth')
      localStorage.removeItem('current_username')
      this.updateAuth()
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
  created: function(){
    this.$router.push({name: "root"})
    this.updateAuth()
  }  
};
</script>

<!-- Representa el css (Estilo) -->
<style>
body {
  margin: 0 0 0 0;
}
.encabezado {
  margin: 0 0 0 0;
  background: linear-gradient(
    90deg,
    rgb(0, 36, 19) 0%,
    rgba(9, 97, 121, 0.541) 100%
  );
  height: 90px;
  padding: 0%;
}
#logo {
  width: 200px;
  position: relative;
  left: 42%;
  top: 10px;
}
nav {
  padding: 3px;
}
nav button {
  width: 130px;
  color: rgb(1, 42, 23);
  background: #a0c28fca;
  border: 1px solid #e5e7e9;
  border-radius: 5px;
  padding: 10px 20px;
}
nav button:hover {
  color: #472834;
  background: #e5e7e9;
  border: 2px solid #e5e7e9;
}
.menu {
  width: 100%;
}
.comp {
  width: 85%;
}
.main-component {
  height: 60vh;
  margin: 0%;
  padding: 0%;
  background: #fdfefe;
}
.footer {
  margin: 0 0 0 0;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px;
  background-color: rgba(9, 97, 121, 0.541);
}
.footer h2 {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: azure;
}

.menu button {
  height: 50px;
  width: 150px;
  background-color: rgb(178, 190, 66);
  color: white;
  font-size: 16px;
}

.botones {
  margin: 0 0 0 0;
}
</style>
