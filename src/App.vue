<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favorite="favorite"/>
  <Favorite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>

  <p v-if="error !== ''">{{error}}</p>
  <p v-if="result !== 0" class="result-text">{{this.result}}</p>

  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
  </div>
</template>

<script>
  import CryptoConvert from 'crypto-convert';
  import Input from './components/Input.vue';
  import Selector from './components/Selector.vue';
  import Favorite from './components/Favorite.vue';

  const cryptoConvert = new CryptoConvert();
  export default {
    components: {Input, Selector, Favorite},
    data(){
      return {
        amount: 0,
        cryptoFirst: '',
        cryptoSecond: '',
        error: '',
        result: 0,
        favs: []
      }
    },
    methods: {
      changeAmount(newAmount){
        this.amount = newAmount;
      },
      setCryptoFirst(cryptoFirst){
        this.cryptoFirst = cryptoFirst;
      },
      setCryptoSecond(cryptoSecond){
        this.cryptoSecond = cryptoSecond;
      },
      async convert() {
        if (this.amount <= 0) {
          this.error = "Enter the number bigger than zero"
          return
        } else if (this.cryptoFirst === "" || this.cryptoSecond === "") {
          this.error = "Choose the currency"
          return
        } else if (this.cryptoSecond === this.cryptoFirst) {
          this.error = "Change other currency"
          return
        }
        this.error = ""

        await cryptoConvert.ready();

        if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'ETH'){
          this.result = cryptoConvert.BTC.ETH(this.amount)
        } else if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'USDT'){
          this.result = cryptoConvert.BTC.USD(this.amount);
        } else if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'BTC'){
          this.result = cryptoConvert.ETH.BTC(this.amount);
        } else if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'USDT'){
          this.result = cryptoConvert.ETH.USD(this.amount);
        } else if(this.cryptoFirst === 'USDT' && this.cryptoSecond === 'BTC'){
          this.result = cryptoConvert.USD.BTC(this.amount);
        } else if(this.cryptoFirst === 'USDT' && this.cryptoSecond === 'ETH'){
          this.result = cryptoConvert.USD.ETH(this.amount);
        }


      },
      favorite(){
        if (this.cryptoSecond !== '' && this.cryptoFirst !== ''){
          this.favs.push({
            "from" : this.cryptoFirst,
            "to" : this.cryptoSecond
          })
        } else{
          this.error = "Choose the currency"
        }
      },
      getFromFavs(index){
        this.setCryptoFirst(this.favs[index].from)
        this.setCryptoSecond(this.favs[index].to)
      }
    }
  }
</script>

<style scoped>
  .selectors{
    display: flex;
    justify-content: space-around;
    width: 700px;
    margin: 0 auto;
  }
</style>