<template>
    <div class="relative bg-white border border-slate-100 rounded-2xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
      <!-- <div @click="onClick" class="absolute top-8 left-8"> -->
        <img :src="isFavorite ? '/like-2.svg' : '/like-1.svg'" alt="Favorite" class="absolute top-6 left-6" @click="addFavorite(item)"/>
      <!-- </div> -->
      <img :src="imageurl" alt="Sneaker" />
      <p class="mt-2">{{title}}</p>
      
      <div class="flex justify-between mt-5">
        <div class="flex flex-col gap-2">
          <span class="text-slate-200">Price:</span>
          <span class="font-bold">{{price}} dram.</span>
        </div>
        <img :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" @click="cartActions(item)" />
      </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
  inject: ['cartActions'],
  props: {
    title: {
      type: String,
      required: false
    },
    imageurl: {
      type: String,
      required: false
    },
    price: {
      type: Number,
      required: false
    },
    isAdded: {
      type: Boolean,
      required: false
    },
    isFavorite: {
      type: Boolean,
      required: false
    },
    item: {
      type: Object,
      required: false
    },
  },
  data() {
    return {
      users: [],
      userName: "",
      userPass: "",
      userEmail: "",
      msgerror: '',
    }
  },
  methods: {

    addFavorite(item) {
      try{
        if(!item.isFavorite) {

          item.isFavorite = true

          axios.post(`https://67e54f4bc6572184.mokky.dev/favorites`, {product_id: item.id})
            .then((response) => { 

              console.log(response.data)
              item.favoriteId = response.data.id

            })
        } else {
          item.isFavorite = false
          console.log(item)
          axios.delete(`https://67e54f4bc6572184.mokky.dev/favorites/${item.favoriteId}`)
            .then((response) => { 

              item.favoriteId = null
              
            })
        }
      } catch(err) {
        console.log(err)
      }


    }
  }
}
</script>