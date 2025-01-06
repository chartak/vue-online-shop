<template>
    <header class="flex justify-between border-b border-slate-300 px-8 py-8">
      <router-link to="/">
        <div class="flex items-center  gap-4">
          <img src="/logo.png" alt="logo" class="w-10"/>
          <div>
            <h2 class="text-xl font-bold uppercase">Men's shoes</h2>
            <p class="text-slate-500">Online store</p>
          </div>
        </div>
      </router-link>


      <ul class="flex items-center gap-10">
        <li @click="openCart" class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black disabled">
          <img src="/cart.svg" alt="Cart" />
          <b>{{ totalPrice }} dram</b>
        </li>

        <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="Favorites" />
          <router-link to="/favorites"><span>Favorites</span></router-link>
        </li>

        <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black">
          <img src="/profile.svg" alt="Profile" />
          <span>Profile</span>
        </li>

        <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black">
          Header menu
          <input type="text" v-model="name">
          <button @click="$emit('closeMenu', name)">Close menu</button>

          <input type="text" 
          :value="modelValue"
          @input="$emit('update:modelValue', $event.target.value)"
          >
        </li>
      </ul>
    </header>
</template>

<script>
export default {
  // emits: ['closeMenu'],
  emits: {
    closeMenu(name) {
      if(!name)
        return false
      else
        return true
    }
  },
  data() {
    return {
      name: ''
    }
  },
  props: {
    modelValue: String,

    openCart: {
      type: Function,
      required: true
    },
    totalPrice: {
      type: Number,
      required: true
    },
  }
}
</script>