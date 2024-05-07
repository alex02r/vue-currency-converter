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
        getFormattedValue(currency, amount){

            const formatter = new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: currency
            });

            return formatter.format(amount);

        },
        getCurrency(value){
            for (let currency in this.currencies) {
                if (this.currencies[currency] === value) {
                    return currency;    
                }
            }
        },
        getValue(amount, from, to){

            from = this.getCurrency(from);
            to = this.getCurrency(to);

            let request = 'latest?amount='+amount+'&from='+from+'&to='+to;
            axios.get(store.api_frankfurter+request).then( response => {
                console.log(response.data.rates[to]);
                if (this.currency_1 == this.currencies[from]) {
                    this.value_2 = response.data.rates[to]
                }else{
                    this.value_1 = response.data.rates[to]
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
                    <h4>{{ getFormattedValue( getCurrency(currency_1), value_1) }} è uguale a</h4>
                    <h2>{{ new Intl.NumberFormat('en-IN', { maximumSignificantDigits: 3 }).format( value_2 ) +' '+getCurrency(currency_2)}} </h2>
                </div>
                <div class="input-group mb-3">
                    <input type="number" name="ammount1" id="ammount1" class="form-control" v-model="value_1" @keyup="getValue(value_1, currency_1, currency_2)">
                    <select class="form-select" name="currency1" id="currency1" v-model="currency_1" @change="getValue(value_1, currency_1, currency_2)">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
                <div class="input-group mb-3">
                    <input type="number" name="ammount2" id="ammount2" class="form-control" v-model="value_2" @keyup="getValue(value_2, currency_2, currency_1)">
                    <select class="form-select" name="currency2" id="currency2" v-model="currency_2" @change="getValue(value_1, currency_1, currency_2)">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>

</style>