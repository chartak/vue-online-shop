<template>
    <div class="flex flex-col gap-4" v-auto-animate>
        <CartItem 
        v-for="c in cart"
        :key="c.id" 
        :itemtitle="c.title"
        :itemprice="c.price"
        :itemurl="c.imageUrl"
        :itemcart="c"
        :removeToCart="deleteToCart"/>
    </div>
</template>

<script>
import CartItem from './CartItem.vue';

export default {
  components: {
    CartItem
  },
  props: {
    cart: {
      type: Array,
      required: false
    },
    deleteToCart: {
      type: Function,
      required: true
    }
  }
}
</script>