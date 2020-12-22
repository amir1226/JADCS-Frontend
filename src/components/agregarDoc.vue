<template>
  <div>
    <b-row class="justify-content-md-center font-weight-bold">
      <b-col>
        <h3>Agregar Documento</h3>
      </b-col>
    </b-row>
    <b-row class="justify-content-md-center mt-5">
      <b-col cols="12" md="2">
        <p class="h5">Radicado</p>
      </b-col>
      <b-col cols="12" md="2">
        <b-form-input type="text" v-model="id_radicado"> </b-form-input>
      </b-col>
      <b-col cols="12" md="2">
        <p class="h5">Fecha de radicación</p>
      </b-col>
      <b-col cols="12" md="2">
        <b-form-input type="text" v-model="Fradicacion"> </b-form-input>
      </b-col>
      <b-col cols="12" md="2">
        <p class="h5">Fecha de vencimiento</p>
      </b-col>
      <b-col cols="12" md="2">
        <b-form-input type="text" v-model="Fvencimiento"> </b-form-input>
      </b-col>
    </b-row>
    <b-row class="justify-content-md-center mt-5">
      <b-col cols="12" md="2">
        <p class="h5">Tipo</p>
      </b-col>
      <b-col cols="12" md="2">
        <b-form-select v-model="tipo" :options="options"></b-form-select>
      </b-col>
      <b-col cols="12" md="2">
        <p class="h5">Status</p>
      </b-col>
      <b-col>
        <b-form-input type="text" v-model="Status"> </b-form-input>
      </b-col>
      <b-col cols="12" md="2">
        <p class="h5">Anexos</p>
      </b-col>
      <b-col cols="12" md="2">
        <b-form-input type="number" v-model="Anexos" min="0"> </b-form-input>
      </b-col>
    </b-row>
    <b-row class="mt-5">
        <b-col cols="12">
          <b-button variant="dark" @click="agregarDocumento" size="lg"
            >Agregar Documento</b-button
          >
        </b-col>
  </div>
</template>
<!--
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
  -->
<script>
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
      options: [
        { value: null, text: "Seleccione una opción" },
        { value: "derecho de peticion", text: "Derecho de petición" },
        { value: "tutelas", text: "Tutelas" },
        { value: "consultas", text: "Consultas" },
      ],
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
</style>