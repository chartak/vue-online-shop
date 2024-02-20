<template>
        <h2>CRYPTO BLOG</h2>
        <input type="number" min="0" @input="changeAmount($event.target.value)" placeholder="Enter Number">
        <button @click="convertor">Change</button>
        <button @click="favourite">Favourite</button>
</template>

<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convertor: {
            type: Function,
            requireq: true
        },
        favourite: {
            type: Function,
            requireq: true
        }
    }
}
</script>

<style scoped>
input {
    outline: none;
    width: 500px;
    position: relative;
    /* top: -50px; */
    font-size: 1.25em;
    border-radius: 5px;
    border: 4px solid #1a032d;
    padding: 15px 20px;
    background: #fafafa;
    color: #333;
}

button {
    position: relative;
    /* top:  -20px; */
    padding: 15px 20px;
    color: #fff;
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
    background: #1a032d;
    border: 0;
    border-radius: 5px;
}

button:hover {
    transform: translateY( -5px);
}
</style>