<template>
  <div>
    <h1 class="font-weight-bold">Sesión iniciada</h1>
    <h2 class="font-weight-light">
      Bienvenido(a) <span> {{ username }} </span>
    </h2>
  </div>
</template>

<script>
export default {
  name: "SesionIn",
  data: function () {
    return {
      username: "",
    };
  },
  methods: {},

  created: function () {
    this.username = localStorage.getItem("current_username");
  },
};
</script>

<style>
</style>