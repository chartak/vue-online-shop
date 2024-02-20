<template>
    <h2>Selected favourits</h2>
    <div @click="getFromFavs(index)" v-for="(el, index) in favs"  :key="index">
        <span>{{ el.from }}</span>
        <span>{{ el.to }}</span>
    </div>
</template>

<script>
export default {
    props: {
        favs: {
            type: Array,
            required: true
        },
        getFromFavs: {
            type: Function,
            required: true
        },
    }
}
</script>

<style scoped>
    h2 {
        color: #524949;
    }
    div {
        display: flex;
        justify-content: space-between;
        width: 500px;
        margin: 15px 20px;
        transition: all 500ms ease;
    }
    div:hover {
        opacity: 0.7;
        transform: scale(1.1);
        cursor: pointer;
    }
    span {
        padding: 15px 20px;
        color: #fff;
        background: #1a032d;
    }

</style>