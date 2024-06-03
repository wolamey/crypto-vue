
<template >
    <input min="0" @input="changeAmount($event.target.value)" type="number">
<br>
    <button @click="convert()">Обменять</button>


    <button @click="favourite()" className="fav-button"> В избранное</button>
</template>


<script >

export default{
    props:{
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        },
        favourite: {
            type: Function,
            required: true
        }
    }
    
}

</script>



<style scoped>

input{
    outline: none;
    background: transparent;
    border: 1px solid white;
    color: white;
    padding: 10px;
    border-radius: 10px;
    margin: auto;
    width: 50%;
}

button{
margin: 20px auto;
background-color: transparent;
padding: 10px;
border: 1px solid white;
    color: white;
border-radius: 10px;
cursor: pointer;

}

button.fav-button{
margin-left: 20px;
}

</style>
