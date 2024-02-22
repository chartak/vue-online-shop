<template>
  <!-- USER BLOG START -->
    <h2>USER BLOG</h2>
    <input type="text" v-model="userName" placeholder="Name">
    <input type="password" v-model="userPass" placeholder="Password">
    <input type="email" v-model="userEmail" placeholder="Email">
    <button @click="sendData()">Sent</button>
    <p v-if="msgerror != ''" style="color: red;">{{msgerror}}</p>
    <User v-for="(el, index) in users" :user="el" :currindex="index" :deleteUser="deleteUser"></User>
  <!-- USER BLOG END -->

  <!-- CRYPTO BLOG START -->
    <hr />
    <Input :changeAmount="changeAmount" :convertor="convertor" :favourite="favourite"/>
    <div>
      <p v-if="error != ''" style="color: red;">{{error}}</p>
      <p v-if="result != ''">{{ result }}</p>
      {{ cryptoFirst }} 
      <span v-if="cryptoSecond != ''"> >>>  {{ cryptoSecond }}</span>
    </div>

    <div className="selectors">
      <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
      <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
    </div>

    <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
  <!-- CRYPTO BLOG END -->
</template>

<script>
import User from './components/User.vue';
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import CryptoConvert from 'crypto-convert';
import Favourite from './components/Favourite.vue';

const convert = new CryptoConvert();

export default {
  components: {
    User, Input, Selector, Favourite
  },
  data() {
    return {
      users: [],
      userName: "",
      userPass: "",
      userEmail: "",
      msgerror: '',

      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: []
    }
  },
  methods: {
    // --------User-----------------
    sendData(){

      if(this.userName.trim() == '') {
        this.msgerror = 'Username is required';
        return;
      } else if(this.userPass.trim() == '') {
        this.msgerror = 'Password is required';
        return;
      } else if(this.userEmail.trim() == '') {
        this.msgerror = 'Email is required';
        return;
      } else {
        if(!this.validateEmail(this.userEmail.trim())) {
          this.msgerror = "Email invalid!";
          return;
        }
      }

      this.msgerror = '';

      this.users.push({
        name: this.userName,
        pass: this.userPass,
        email: this.userEmail,
      })
    },
    validateEmail(email) {
      if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email)) {
        return true;
      } else {
        return false;
      }
    },
    deleteUser(index){
      this.users.splice(index, 1);
    },
    // --------Crypto-----------------
    changeAmount(val){
      this.amount = val;
    },
    setCryptoFirst(val){
      this.cryptoFirst = val;
    },
    setCryptoSecond(val){
      this.cryptoSecond = val;
    },
    favourite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      })
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
    async convertor() {
      if(this.amount <= 0){
        this.error = "Insert amount"
        return;              
      } else if(this.cryptoFirst == "") {
        this.error = "Select First crypto"
        return;
      } else if(this.cryptoSecond == "") {
        this.error = "Select Second crypto"
        return;
      } else if(this.cryptoFirst == this.cryptoSecond) {
        this.error = "Choose another cryptocurrency"
        return;
      }   
      
      this.error='';

      await convert.ready();

      if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH') {

        this.result = convert.BTC.ETH(this.amount);

      } else if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT') {

        this.result = convert.BTC.USD(this.amount);

      } else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC') {

        this.result = convert.ETH.BTC(this.amount);

      } else if(this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT') {

        this.result = convert.ETH.USD(this.amount);

      } else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC') {

        this.result = convert.USD.BTC(this.amount);

      } else if(this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH') {

        this.result = convert.USD.ETH(this.amount);

      }

    }

  }
}
</script>


<style scoped>
.selectors {
  display: flex;
  /* justify-content: space-around;
  width: 700px; */
  margin: 0 auto;
}
</style>