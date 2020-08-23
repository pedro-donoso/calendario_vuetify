<template>
  <div class="container-fluid" id="contador">
    <h6>Propiedad Computada</h6>
    <h3>Contador:</h3>
    <h1>{{cantidad}}</h1>
    <v-btn x-small rounded color="blue" @click="aumentar">Aumentar</v-btn> |
    <v-btn x-small rounded color="error" @click="reducir">Reducir</v-btn>
  </div>
</template>

<script>
export default {
  methods: {
    aumentar() {
      this.$store.state.cantidad++;
    },
    reducir() {
      this.$store.state.cantidad--;
    },
  },

  computed: {
    cantidad() {
      return this.$store.state.cantidad;
    },
  },
};
</script>

<style lang="scss" scoped>
#contador {
  font-family: "Courier New", Courier, monospace;
  text-align: center;
  background: greenyellow;
}
</style>