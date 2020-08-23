<template>
  <v-app>
    <div class="contador">
      <contador></contador>
    </div>

    <v-content class="calendario">
      <v-container>
        <router-view />
        <v-dialog v-model="loading.estado" hide-overlay persistent width="300">
          <v-card :color="loading.color" dark>
            <v-card-text>
              {{loading.titulo}}
              <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-container>
    </v-content>

    <div class="computada">
      <div class="container">
        <h3>Hecho por: {{ nombre }} {{ apellidos }}</h3>
        <h3>{{ profesion }} | {{ ciudad }}</h3>
      </div>
    </div>
  </v-app>
</template>

<script>
import Contador from "../src/components/Contador.vue";

import { mapState } from "vuex";

export default {
  name: "App",
  components: { Contador },

  computed: {
    nombre() {
      return this.$store.state.nombre;
    },

    apellidos() {
      return this.$store.state.apellidos;
    },

    profesion() {
      return this.$store.state.profesion;
    },

    ciudad() {
      return this.$store.state.ciudad;
    },

    ...mapState(["loading"]),
  },
};
</script>

<style lang="scss" scoped>
.calendario {
  background: gray;
}

.computada {
  background: orangered;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  color: #fff;
  text-align: left;
}
</style>