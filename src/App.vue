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
      loading: true
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
        this.loading = false;
      })
    }
  },
}
</script>
<template lang="">
  <main>
    <div class="spinner" v-if="loading"></div>
    <AppFromConverter v-else :currencies="currencies" />
  </main>
</template>
<style lang="scss">
  @use './styles/generals.scss';
  .spinner {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: conic-gradient(#0000 10%,#474bff);
    -webkit-mask: radial-gradient(farthest-side,#0000 calc(100% - 9px),#000 0);
    animation: spinner-zp9dbg 1s infinite linear;
 }
 
 @keyframes spinner-zp9dbg {
    to {
       transform: rotate(1turn);
    }
 }

</style>