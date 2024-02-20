<template>
    <ul>
        <li @click="setCrypto('BTC')" :className="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="setCrypto('ETH')" :className="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
        <li @click="setCrypto('USDT')" :className="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
    </ul>

</template>

<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        cryptoNow: {
            type: String,
            required: true
        }
    },
    // data() {
    //     return {
    //         current: ''
    //     }
    // },
    // methods: {
    //     selectItem(val){
    //         this.current = val;
    //         this.setCrypto(val)
    //     }
    // }
}
</script>

<style scoped>
    ul {
        list-style: none;
        width: 200px;
        padding: 0;
        border-radius: 3px;
        border: 3px solid #000;
        
    }
    li {
        display: block;
        background: #1A032D;
        color: #fff;
        padding: 20px 5px;
    }
    li:hover, li.active {
        background: #ad8dc7;
        cursor: pointer;
    }
</style>