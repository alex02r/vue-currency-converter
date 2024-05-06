<script>
import { store } from '../store';
import axios from 'axios';

export default {
    props:{
        currencies: Object
    },
    data() {
        return {
            store,
            currency_1: "Euro",
            currency_2: "United States Dollar",
            value_1: 1,
            value_2: 0,
        }
    },
    mounted() {
        this.getValue( this.value_1, this.currency_1, this.currency_2)
    },
    methods: {
        getValue(amount, from, to){
            let valutaInvertita = {};

            // Iterazione attraverso l'oggetto originale
            for (let chiave in this.currencies) {
                if (this.currencies.hasOwnProperty(chiave)) {
                    let valore = this.currencies[chiave];
                    valutaInvertita[valore] = chiave;
                }
            }
            let request = 'latest?amount='+amount+'&from='+valutaInvertita[from]+'&to='+valutaInvertita[to];
            axios.get(store.api_frankfurter+request).then( response => {
                console.log(response.data.rates[valutaInvertita[to]]);
                if (this.currency_1 == from) {
                    this.value_2 = response.data.rates[valutaInvertita[to]]
                }else{
                    this.value_1 = response.data.rates[valutaInvertita[to]]
                }
            })
        }
    },
}
</script>
<template lang="">
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1>Currency Converter</h1>
            </div>
            <div class="col-12 col-md-6">
                <div class="">
                    <h4>Resoconto</h4>
                    <h2>Valuta</h2>
                </div>
                <div class="">
                    <input type="number" name="ammount1" id="ammount1" class="" v-model="value_1" @keyup="getValue(value_1, currency_1, currency_2)">
                    <select name="currency1" id="currency1" v-model="currency_1" @change="getValue(value_1, currency_1, currency_2)">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
                <div class="">
                    <input type="number" name="ammount1" id="ammount1" class="" v-model="value_2" @keyup="getValue(value_2, currency_2, currency_1)">
                    <select name="currency2" id="currency2" v-model="currency_2" @change="getValue(value_1, currency_1, currency_2)">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="">
    
</style>