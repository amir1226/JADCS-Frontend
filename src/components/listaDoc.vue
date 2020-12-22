<template>
  <div>
    <div v-if="lista_documentos.length > 0">
      <table class="table-responsive table-striped text-center text-capitalize">
        <thead class="thead-dark">
          <tr>
            <th>Número Radicado</th>
            <th>Fecha de entrada</th>
            <th>Fecha de vencimiento</th>
            <th>Tipo de Documento</th>
            <th>Status</th>
            <th>Número de anexos</th>
            <th>Días Restantes</th>
          </tr>
        </thead>
        <tr v-for="documento in lista_documentos">
          <td>{{ documento.id_radicado }}</td>
          <td>{{ documento.fecha_radicacion }}</td>
          <td>{{ documento.fecha_vencimiento }}</td>
          <td>{{ documento.tipo }}</td>
          <td>{{ documento.status }}</td>
          <td>{{ documento.anexos }}</td>
          <td class="semaforo">
            <p id="verde" v-if="documento.semaforo == 'verde'" class="mt-1"></p>
            <p
              id="amarillo"
              v-else-if="documento.semaforo == 'amarillo'"
              class="mt-1"
            ></p>
            <p
              id="rojo"
              v-else-if="documento.semaforo == 'rojo'"
              class="mt-1"
            ></p>
          </td>
        </tr>
      </table>
    </div>
    <div v-else>
      <table id="TablaVacia">
        <tr>
          <th><h3>No tiene documentos asignados</h3></th>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "listaDoc",
  components: {},
  data: function () {
    return {
      lista_documentos: [],
    };
  },
  created() {
    let username = localStorage.getItem("current_username");
    axios
      .get("https://jadcs-backend.herokuapp.com/resumendoc/" + username)
      .then((response) => {
        this.lista_documentos = response.data;
      })
      .catch((error) => {
        console.log("error");
        alert("No se puede mostrar lista");
      });
  },
};
</script>

<style>
.semaforo {
  border-radius: 100%;
  width: 20px;
  height: 20px;
}

.semaforo #verde {
  background-color: green;
}
.semaforo #amarillo {
  background-color: yellow;
}

.semaforo #rojo {
  background-color: red;
}
</style>