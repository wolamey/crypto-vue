<template>
    <ul>
        <li @click="setCrypto('BTC')" :className="cryptoNow === 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="setCrypto('ETH')" :className="cryptoNow === 'ETH' ? 'active' : ''">Eth</li>
        <li @click="setCrypto('USDT')" :className="cryptoNow === 'USDT' ? 'active' : ''">USDT</li>
    </ul>
</template>


<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        cryptoNow:{
            type: String,
            required: true
        }
    }

}

</script>



<style scoped>
ul {
    /* margin: 20px auto; */

    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 1px solid #ffffff;
}

li {
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    display: block;
    background: transparent;
    color: #fff;
    padding: 20px 0;
}

li:hover,
li.active {
    background: #000000;
    cursor: pointer;
}
</style>
