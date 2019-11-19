<template>
    <div>
        <h1>Conversiones</h1>
        <label >Moneda Base</label>
        <select name="select" v-model="monedaBase">
            <option value="valor" selected>---------------</option>
            <option value="USD">USD-Dolar Americano</option>
            <option value="AUD">AUD - Dólar Australiano</option>
            <option value="CAD">CAD - Dólar Canadiense</option>
            <option value="EUR">EUR - Euro</option>
            <option value="GBP">GBP - Libra Esterlina</option>
        </select><br>
        <label >Ingrese el Monto Base</label> <br>
        <input type="number" v-model="valor" min="0"><br>
        <label >Moneda Cambio</label>
        <select name="select" v-model="monedaNueva" @change="cambio">
            <option value="valor" selected>---------------</option>
            <option value="USD">USD-Dolar Americano</option>
            <option value="AUD">AUD - Dólar Australiano</option>
            <option value="CAD">CAD - Dólar Canadiense</option>
            <option value="EUR">EUR - Euro</option>
            <option value="GBP">GBP - Libra Esterlina</option>
        </select><br>
        <label >Valor final</label><br>
        <p>{{monedaNueva}} {{intercambio*valor}}</p>
    </div>
</template>

<script>
    // eslint-disable-next-line no-unused-vars
    import axios from 'axios';
    export default {
        name: "Moneda",
        data: function () {
          return{
              valor: '',
              monedaBase:'',
              monedaNueva: '',
              intercambio: {}
          }
        },
        methods:{
            cambio(){
                axios.get(`https://api.exchangerate-api.com/v4/latest/${this.monedaBase}`)
                    .then((res) => {
                        this.intercambio = res.data.rates[this.monedaNueva];
                    })
            }
        },
        mounted() {
            if (this.monedaBase){
                this.nuevoValor()
            }
        }
    }
</script>

<style scoped>
    select{
        height: 50px;
        margin: 60px;
        width: 60%;
    }
    input{
        height: 30px;
        width: 80%;
    }
</style>