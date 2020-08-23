<template>
  <div class="contador">
    <h3 class="contador__titulo">Selecciona fecha y consulta valor del dolar: </h3>
    <v-layout :wrap="true">
      <v-flex xs12>
        <v-card>
          <v-date-picker
            v-model="fecha"
            full-width
            locale="es-cl"
            :min="minimo"
            :max="maximo"
            @change="getDolar(fecha)"
          ></v-date-picker>
        </v-card>
        <v-card color="info" dark>
          <v-card-text class="display-1 text-center">{{valor}}</v-card-text>
        </v-card>
      </v-flex>
    </v-layout>

    <h4 class="contador__texto">* NO se dispone de datos de los días sábados y domingos</h4>
    <h4 class="contador__texto">** El cambio corresponde a Pesos CLP</h4>
  </div>
</template>

<script>
import axios from "axios";
import { mapMutations } from "vuex";
export default {
  data() {
    return {
      fecha: new Date().toISOString().substr(0, 10),
      minimo: "1984",
      maximo: new Date().toISOString().substr(0, 10),
      valor: null,
    };
  },
  methods: {
    ...mapMutations(["mostrarLoading", "ocultarLoading"]),

    async getDolar(dia) {
      let arrayFecha = dia.split(["-"]);
      let ddmmyy = arrayFecha[2] + "-" + arrayFecha[1] + "-" + arrayFecha[0];

      try {
        this.mostrarLoading({
          titulo: "Accediendo a información",
          color: "secondary",
        });

        let datos = await axios.get(
          `https://mindicador.cl/api/dolar/${ddmmyy}`
        );

        if (datos.data.serie.length > 0) {
          this.valor = await datos.data.serie[0].valor;
        } else {
          this.valor = "Sin resultados";
        }
      } catch (error) {
      } finally {
        this.ocultarLoading();
      }
    },
  },
  created() {
    this.getDolar(this.fecha);
  },
};
</script>

<style lang="scss" scoped>

.contador__titulo{
  color: #fff;
  background: blueviolet;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

.contador__texto {
  color: red;
  text-align: center;
}
</style>
