<template>
    <h3>{{ count }}</h3>
    <button @click="increment">+</button>
        
</template>

<script setup>
    import {ref} from 'vue';

    const count = ref(0);

    function increment(){
        count.value++;
        console.log(count);
    }

// export default {
//     data() {
//         return {
//             count: 0
//         }
//     },
//     methods: {
//         increment() {
//             this.count++
//         }
//     }
// }
</script>

<style scoped>

</style>