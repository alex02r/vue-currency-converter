<script>
export default {
    props:{
        currencies: Object
    },
    data() {
        return {
            currency_1: "Euro",
            currency_2: "United States Dollar",
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
                    <input type="number" name="ammount1" id="ammount1" class="">
                    <select name="currency1" id="currency1" v-model="currency_1">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
                <div class="">
                    <input type="number" name="ammount1" id="ammount1" class="">
                    <select name="currency2" id="currency2" v-model="currency_2">
                        <option v-for="(currency, index) in currencies" :key="index" :value="currency">{{ currency }}</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="">
    
</style>