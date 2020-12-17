<template>
  <div>
    <div v-if="lista_documentos.length > 0">
      <table id="TablaDocumentos">
        <tr>
          <th>Número Radicado</th>
          <th>Fecha de entrada</th>
          <th>Fecha de vencimiento</th>
          <th>Tipo de Documento</th>
          <th>Status</th>
          <th>Número de anexos</th>
          <th id="oculta">Dias Restantes</th>
        </tr>
        <tr v-for="documento in lista_documentos">
          <td>{{ documento.id_radicado }}</td>
          <td>{{ documento.fecha_radicacion }}</td>
          <td>{{ documento.fecha_vencimiento }}</td>
          <td>{{ documento.tipo }}</td>
          <td>{{ documento.status }}</td>
          <td>{{ documento.anexos }}</td>
          <td class="semaforo">
            <p id="verde" v-if="documento.semaforo == 'verde'"></p>
            <p id="amarillo" v-else-if="documento.semaforo == 'amarillo'"></p>
            <p id="rojo" v-else-if="documento.semaforo == 'rojo'"></p>
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
#TablaDocumentos {
  border: 6px solid black;
  text-transform: capitalize;
  text-align: center;
}

#TablaVacia {
  width: 700px;
  text-align: left;
}

#TablaVacia th {
  padding: 30px;
  color: rgb(100, 167, 46);
  font-size: 20px;
}

#TablaDocumentos th {
  border: 1px solid black;
  background: linear-gradient(rgb(3, 61, 34) 0%, rgba(5, 72, 90, 0.541) 100%);
  color: rgba(242, 242, 248, 0.931);
  width: 120px;
}

#TablaDocumentos td {
  border: 1px solid black;
}

.semaforo #verde {
  border-radius: 100%;
  width: 20px;
  height: 20px;
  background-color: green;
  position: relative;
  left: 50px;
}
.semaforo #amarillo {
  border-radius: 100%;
  width: 20px;
  height: 20px;
  background-color: yellow;
  position: relative;
  left: 50px;
}

.semaforo #rojo {
  border-radius: 100%;
  width: 20px;
  height: 20px;
  background-color: red;
  position: relative;
  left: 50px;
}
</style>