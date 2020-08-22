<template>
  <v-app>
   

    <contador></contador>

    <v-content>
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


<div class="container">
  <h3>Hola me llamo: {{ nombre }}</h3>
    <h3>Mis apellidos son: {{ apellidos }}</h3>
    <h3>Mi profesión es: {{ profesion }}</h3>
    <h3>Vivo en la Ciudad de: {{ ciudad }}</h3>
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

    // accede al store
    nombre(){
      return this.$store.state.nombre
    },

    apellidos(){
      return this.$store.state.apellidos
    },

    profesion(){
      return this.$store.state.profesion
    },

    ciudad(){
  return this.$store.state.ciudad
    },

    ...mapState(["loading"])
  },


  




};
</script>
