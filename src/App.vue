<template>
  <h1>CRYPTO</h1>

  <p className="error" v-if="error !== ''">{{ error }}</p>
  <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite" />
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
  </div>

  <h2 v-if="result !== 0">{{ result }}</h2>

  <Favourite :favs="favs" :getFromFavs="getFromFavs" v-if="favs.length > 0" />

</template>


<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue'
import CryptoConvert from 'crypto-convert';
import Favourite from './components/Favourite.vue'


const convert = new CryptoConvert();

export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favs: [],
    }
  },
  methods: {
    favourite() {
      if (this.cryptoFirst === '' || this.cryptoSecond === '') {
        this.error = 'Необходимо выбрать криптопару';
        return;
      }
      this.error = '';
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond,
      })
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
      this.convert()
    },
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Сумма должна быть больше 0';
        return;
      }

      if (this.cryptoFirst === this.cryptoSecond) {
        this.error = 'Выберите разные валюты';
        return;
      }


      if (this.cryptoFirst === '' || this.cryptoSecond === '') {
        this.error = 'Необходимо выбрать валюты';
        return;
      }


      this.error = '';
      await convert.ready()

      if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH') this.result = convert.BTC.ETH(this.amount);
      else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
        this.result = convert.BTC.USDT(this.amount);
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC') this.result = convert.ETH.BTC(this.amount);
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
        this.result = convert.ETH.USDT(this.amount);
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC') this.result = convert.USDT.BTC(this.amount);
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH') this.result = convert.USDT.ETH(this.amount);



    }
  }
}

</script>



<style scoped>
.selectors {
  width: 80%;
  margin: 20px auto;
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.error {
  margin: 0 0 30px 0;
  font-size: 20px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: red;
}
</style>
