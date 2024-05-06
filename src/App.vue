<script>
import axios from 'axios';
import { store } from './store';
import AppFromConverter from './components/AppFromConverter.vue';
export default {
  components:{
    AppFromConverter
  },
  data() {
    return {
      store,
      currencies: {},
    }
  },
  mounted() {
    this.getCurrencies();
  },
  methods: {
    //funzione che prende l'oggetto di tutte le valute
    getCurrencies(){
      axios.get(store.api_frankfurter+'currencies').then( response =>{
        this.currencies = response.data;
      })
    }
  },
}
</script>
<template lang="">
  <main>
    <AppFromConverter :currencies="currencies" />
  </main>
</template>
<style lang="scss">
  @use './styles/generals.scss';

</style>