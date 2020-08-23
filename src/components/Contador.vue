<template>
 <div class="container" id="contador">
<h6>Propiedad Computada</h6>
 <h1>Contador: {{cantidad}}</h1>
 <v-btn rounded color="blue" @click="aumentar">Aumentar</v-btn> |
  <v-btn rounded color="error" @click="reducir">Reducir</v-btn>
 </div>
</template>

<script>
export default {

//props: ['cantidad'],
methods: {
    aumentar(){
        //this.$emit('aumentar');
        this.$store.state.cantidad++;
    },
    reducir(){
        //this.$emit('reducir');
        this.$store.state.cantidad--;
    }
},

computed: {
    cantidad(){
        return this.$store.state.cantidad;
    }
},

}
</script>

<style lang="scss" scoped>
#contador{
    font-family: 'Courier New', Courier, monospace;
}
</style>