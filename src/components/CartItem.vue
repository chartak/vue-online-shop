<template>
    <div class="relative flex w-full border border-slate-200 rounded-xl p-4 gap-4">
      <img :src="itemurl"  class="w-16 h-16" alt="Sneaker" />
      <div class="flex flex-col w-full">
        <p>{{ itemtitle }}</p>
        <div class="flex justify-between mt-5">
          <span class="font-bold">{{itemprice}} руб.</span>
          <img 
            @click="removeToCart(itemcart)"
            class="cursor-pointer opacity-30 hover:opacity-100 transition"
            src="/close.svg"
            alt="Close"
          />
        </div>
      </div>
    </div>
  </template>

<script>
export default {
  props: {
    itemtitle: {
      type: String,
      required: false
    },
    itemurl: {
      type: String,
      required: false
    },
    itemprice: {
      type: Number,
      required: false
    },
    itemcart: {
      type: Object,
      required: false
    },
    removeToCart: {
      type: Function,
      required: false
    },
  }
}
</script>