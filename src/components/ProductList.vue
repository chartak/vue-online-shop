<template>
    <div class="grid grid-cols-4 gap-5" v-auto-animate>
        <Product v-for="product in products" 
          :key="product.id"
          :title="product.title" 
          :imageurl="product.imageUrl" 
          :price="product.price" 
          :isAdded=product.isAdded 
          :isFavorite=product.isFavorite 
          :item="product" 

          />
    </div>
</template>

<script>
import Product from './Product.vue';

export default {

  components: {
    Product
  },
  props: {
    products: {
      type: Array,
      required: false
    }
  }
}
</script>