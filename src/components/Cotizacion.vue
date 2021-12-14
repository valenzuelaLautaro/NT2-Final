<template>

  <section class="src-components-cotizacion">
    <h2>Conversor a dólares</h2>
    <label for="entrada">Ingrese monto $</label>
    <input type="text" id="entrada" v-model="entrada">
    <br>
    <br>
    <label for="valor">Valor del dolar en $</label>
    <input type="text" id="valor" value="200" v-model="cotizacion">
    <span>Actualizacion</span>
    <input type="checkbox" v-model="habilitado">
    <b><span>{{ dameFecha() }}</span></b>
    <br>
    <br>
    <p>Valor convertido en USD {{ resultado() }} </p>
    <br>
    <br>
    <br>
    <h3>RESPUESTAS</h3>
    <p>1: C</p>
    <p>2: B</p>
    <p>3: C</p>
    <p>4: A</p>
    <p>5: C</p>

  </section>

</template>

<script>

  export default  {
    name: 'src-components-cotizacion',
    props: [],
    mounted () {
      this.pedirCotizacion()
    },
    data () {
      return {
        url: 'https://www.dolarsi.com/api/api.php?type=valoresprincipales',
        cotizacion: 0,
        entrada: 0,
        habilitado: false
      }
    },
    methods: {
      async pedirCotizacion(){
        try {
          let respuesta = await this.axios(this.url)
          console.log('Respuesta', respuesta.data[0].casa.venta)
          this.cotizacion = respuesta.data[0].casa.venta
        } catch (error) {
          console.error(error.message)
        }
      },
      resultado(){
        return (parseInt(this.entrada) / parseInt(this.cotizacion)).toFixed(2)
      },
      dameFecha(){
        if(this.habilitado){
          setInterval(this.pedirCotizacion(), 2000)
          return new Date().toLocaleString()
        }
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">

</style>
