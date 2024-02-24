<template>
  <ul>
    <li @click="setCrypto('BTC')" :className='cryptoNow === "BTC" ? "active" : ""'>Bitcoin</li>
    <li @click="setCrypto('ETH')" :className='cryptoNow === "ETH" ? "active" : ""'>ETH</li>
    <li @click="setCrypto('USDT')" :className='cryptoNow === "USDT" ? "active" : ""'>USDT</li>
  </ul>
</template>

<script>
export default {
  props:{
    setCrypto:{
      type: Function,
      required: true
    },
    cryptoNow:{
      type:String,
      required: true
    }
  }
}

</script>

<style scoped>
  ul{
    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 3px solid #000;
  }
  li{
    display: block;
    background: #22C1C350;
    color: #fff;
    padding: 20px 0;
  }

  .active{
    background: #28b685;
    cursor: pointer;
  }


  li:hover, li:active {
    background: #28b685;
    cursor: pointer;
  }
</style>