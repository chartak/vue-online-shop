<template>
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Shoes</h2>
        
        <div class="flex gap-4">
          <select @change="onChangeSelect" class="bg-white py-2 px-3 border rounded-md outline-none">
            <option value="">--Sort By--</option>
            <option value="title">By Name</option>
            <option value="price">By price(<)</option>
            <option value="-price">By price(>)</option>
          </select>
        
          <div class="relative">
            <img class="absolute left-3 top-3" src="/search.svg"/>
            <input @input="onChangeInput" class="border rounded-md py-2 pl-12 pr-4 outline-none focus:border-gray-400" 
            type="text"
            placeholder="Search..." />
          </div>
        </div>
      </div>
      <ProductList :products="products" />

</template>

<script>

import ProductList from '../components/ProductList.vue';
import axios from 'axios';

export default {
  components: {
    ProductList
  },
  data() {
    return {
      products: [],
      filters: [{sortBy: ""},{searchQuery: ""}],
    }
  },
  props: {
    // cartActions: {
    //     type: Function,
    //     required: true
    // },
    // products: {
    //     type: Array,
    //     required: true
    // }
  },
  mounted(){
      this.getProductsList();

      // console.log('a')
      // localStorage.setItem('cart', JSON.stringify(this.cart))
  },
  provide() {
    return {
      //products: this.products,
    }
  },
   methods: {
    onChangeSelect(event){

        this.filters.sortBy = event.target.value

        this.getProductsList()
    },

    onChangeInput(event){

        this.filters.searchQuery = event.target.value

        this.getProductsList()
    },

    getProductsList(){
      let filterQuery = ''

      if(this.filters.sortBy !== undefined && this.filters.sortBy.trim() != "")  {

        filterQuery += "sortBy=" + this.filters.sortBy.trim()
      } 

      if(this.filters.searchQuery !== undefined && this.filters.searchQuery.trim() != "")  {

        filterQuery += "&title=*" + this.filters.searchQuery.trim()+"*"
      }

      try{
          axios.get(`https://67e54f4bc6572184.mokky.dev/products?${filterQuery}`)
          .then((response) => { 

            this.products = response.data 
            console.log(response.data)

          })
        } catch (error) {
          console.log(error);
        }
      }
  }
}
</script>