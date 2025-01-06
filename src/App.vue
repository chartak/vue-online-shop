<template>
  <Drawer v-if="drawerOpen" :closeDrawer="closeDrawer" 
    :cart="cart" :deleteToCart="cartActions"
    :total-price="totalPrice" :tax-persent="taxPersent" />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <button @click="isMenuOpen=true">Open menu </button> {{ nn }}
    <Header :total-price="totalPrice" :openCart="openDrawer" v-if="isMenuOpen" @closeMenu="openClose" v-model="nn"/>

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Drawer from './components/Drawer.vue';

export default {
  components: {
    Header, Drawer
  },
  data() {
    return {
      isMenuOpen: false,
      cart: [],
      drawerOpen: false,
      nn: ''
      // products: []
    }
  },
  computed: {

    totalPrice(){
      return this.cart.reduce((a,item) => a + item.price, 0)
    },

    taxPersent() {
      return Math.round((this.totalPrice * 5)/100)
    },

  },
  methods: {
    openClose(dt){
      this.isMenuOpen=false
      console.log(dt)
      this.nn = dt
    },
    //-----Shopping Cart START-------
    openDrawer(){
      this.drawerOpen = true
    },
    closeDrawer(){
        this.drawerOpen = false
    },

 
    addToCart(item) {
        item.isAdded = true
        this.cart.push(item)
    },
    deleteToCart(item) {
      this.cart.splice(this.cart.indexOf(item), 1)
      item.isAdded = false
    },

    cartActions(item) {
      if(!item.isAdded) {
        this.addToCart(item)
      } else { 
        this.deleteToCart(item)
      }
    },
  //-----Shopping Cart END-------
  },

  provide() {
    
    return {
      // products: this.products,
      cartActions: this.cartActions
    }

  },
  watch: {
    // cart: function() {
    //   console.log('kkkk')
    //   this.products.map((prod) => {
    //     if(prod.isAdded) {
    //       prod.isAdded = false
    //     }
    //   })
      
    // },
    
    // searchQuery(val){
    //   try{
    //     axios.get(`https://67e54f4bc6572184.mokky.dev/products?title=` + `*` + val.trim() + `*`)
    //     .then((response) => { 
    //       this.products = response.data 
    //       console.log(response.data)
    //     })
    //   } catch (error) {
    //     console.log(error);
    //   }
    // }
  }
}
</script>