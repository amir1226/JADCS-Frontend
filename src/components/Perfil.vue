<template>
  <div id="Perfil">
    <div class="Info Usuario">
      <h2>PERFIL DEL USUARIO</h2>
      <table>
        <tr>
          <td>Usuario:</td>
          <td>{{ username }}</td>
        </tr>
        <tr>
          <td>Nombre:</td>
          <td>{{ Nombre }}</td>
        </tr>
        <tr>
          <td>Apellido:</td>
          <td>{{ Apellido }}</td>
        </tr>
        <tr>
          <td>Categoria:</td>
          <td>{{ Categoria }}</td>
        </tr>
      </table>

      <div v-if="esJefe">
        <h3>Personal a cargo:</h3>
        <h3>{{ test }}</h3>
        <ul>
          <li v-for="(persona, index) in Equipo" :key="index">
            {{ persona }}
          </li>
        </ul>
      </div>
    </div>

    <div class="ListaDocumentos">
      <ListaDoc />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ListaDoc from "./listaDoc.vue";
export default {
  name: "Perfil",
  data: function () {
    return {
      username: "",
      Nombre: "",
      Apellido: "",
      Categoria: "",
      Equipo: "",
      esJefe: this.esJefe,
    };
  },
  components: { ListaDoc },
  created: function () {
    this.username = this.$route.params.username;
    let self = this;
    axios
      .get(
        "https://jadcs-backend.herokuapp.com/usuario/perfil/" + this.username
      )
      .then((result) => {
        self.perfil = result.data.Perfil;
        self.Nombre = self.perfil.Nombre;
        self.Apellido = self.perfil.Apellido;
        self.Categoria = self.perfil.Categoria;
        self.Equipo = self.perfil.Equipo;
        if (typeof self.Equipo == "object") {
          self.esJefe = true;
        } else {
          self.esJefe = false;
        }
      })
      .catch((error) => {
        alert("ERROR Servidor");
      });
  },
};
</script>

<style>
#Perfil {
  width: 98%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  color: rgb(2, 71, 39);
}
.ListaDocumentos {
  margin-top: 20px;
}
</style>