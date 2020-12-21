<template>
  <div class="AgregarDocumentos">
    <h2>Agregar Documento</h2>
    <table>
      <tr id="Primera Fila">
        <td>
          <label for="">Radicado</label>
        </td>
        <td>
          <input type="text" v-model="id_radicado" />
        </td>
        <td>
          <label for="">F. de radicación</label>
        </td>
        <td>
          <input type="text" v-model="Fradicacion" />
        </td>
        <td>
          <label for="">F. de vencimiento</label>
        </td>
        <td>
          <input type="text" v-model="Fvencimiento" />
        </td>
      </tr>

      <tr id="Segunda Fila">
        <td>
          <label for="">Tipo</label>
        </td>
        <td>
          <select v-model="tipo">
            <option value="derecho de peticion">Derecho de petición</option>
            <option value="tutelas">Tutelas</option>
            <option value="consultas">Consultas</option>
          </select>
        </td>
        <td>
          <label for="">Status</label>
        </td>
        <td>
          <input type="text" v-model="Status" />
        </td>
        <td>
          <label for="">Anexos</label>
        </td>
        <td>
          <input type="number" min="0" v-model="Anexos" />
        </td>
      </tr>
    </table>
    <button v-on:click="agregarDocumento" id="Agregar">Agregar</button>
  </div>
</template>

<script>
//Prueba
import axios from "axios";
export default {
  name: "AgregarDoc",
  components: {},
  data: function () {
    return {
      id_radicado: "",
      Fradicacion: "",
      Fvencimiento: "",
      tipo: "",
      Status: "",
      Anexos: 0,
    };
  },
  methods: {
    agregarDocumento: function () {
      let username = localStorage.getItem("current_username");
      var tipoDoc = this.tipo;
      if (tipoDoc == 1) {
        tipoDoc = "derecho de peticion";
      } else if (tipoDoc == 2) {
        tipoDoc = "tutelas";
      } else if (tipoDoc == 3) {
        tipoDoc = "consultas";
      }

      var elJson = {
        id_radicado: this.id_radicado,
        fecha_radicacion: this.Fradicacion,
        fecha_vencimiento: this.Fvencimiento,
        tipo: tipoDoc,
        status: this.Status,
        anexos: this.Anexos,
      };
      axios
        .post(
          "https://jadcs-backend.herokuapp.com/cargar/documento?nombre=" +
            username,
          elJson
        )
        .then((response) => {
          alert("Documento cargado en la lista de " + username);
        })
        .catch((err) => {
          console.log(err);
          alert("Error en la carga de documento");
        });
    },
  },
};
</script>

<style>
.AgregarDocumentos {
  color: rgb(2, 71, 39);
}

.AgregarDocumentos table {
  position: relative;
  left: 7%;
  border-spacing: 10px;
}
.AgregarDocumentos button {
  background-color: rgb(110, 108, 69);
  color: azure;
  box-shadow: 5px;
  margin-top: 25px;
  width: 150px;
}

#Agregar {
  height: 60px;
  position: relative;
  left: 35%;
  border-radius: 5px;
}
</style>