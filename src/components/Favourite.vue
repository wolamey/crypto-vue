<template>
    <h3>Варианты в избранном</h3>

    <div @click="getFromFavs(index)" className="favs-wrapper" v-for="(el, index) in favs" :key="index">
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
getFromFavs:{
    type: Function,
    required:true
}
    }

}

</script>



<style scoped>

span{
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    color: white;
    background-color: rgba(0, 0, 0, 0.655);
    padding: 20px;
}
.favs-wrapper{
    display: flex;
    gap: 20px;
    margin: auto;
    width: fit-content;
    background-color: rgba(237, 237, 237, 0.392);
    padding: 20px;

    cursor: pointer;

}
</style>
