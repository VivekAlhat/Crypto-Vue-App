<template>
<div class="hello">
  <div class="title-main">
    <h2>Cryptocurrency Price Indicator</h2>
  </div>
  <div id="crypto-container" v-for="(value, key) in cryptos"  :key="value.key">
    <span class="left">{{ key }}</span>
    <span class="right">₹ {{ value.INR }}</span>
  </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'hello',
  data: () => ({
    cryptos: [],
    errors: []
  }),
  created () {
    axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,BSV,BCH,BNB,XMR,LINK,PAX,EOS,ETC,LTC&tsyms=INR')
      .then(response => {
        this.cryptos = response.data
        console.log(response)
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #f1f1f1;
}

h2 {
  color: black;
  padding-bottom: 10px;
  font-family: monospace;
  font-size: 30px;
  letter-spacing: 2px;
}

div#crypto-container {
  background: white;
  width: 50%;
  height: 65px;
  margin: 0 auto 4px auto;
  padding: 1em;
  box-shadow: 1px 1px 0 lightgrey;
}

span.left {
  padding-top: 5px;
  text-align: center;
  float: left;
  font-weight: bold;
}

span.right {
  padding-top: 5px;
  float: right;
}
</style>
