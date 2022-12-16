<script setup>
import { reactive } from 'vue'

const shoe = reactive({
    name: "",
    img: "",
    startDate: null,
    estKm: 0,
    currentKm: 0
});

function onFileChange(e) {
    var file = document.querySelector('input[type=file]').files[0];

    var files = e.target.files || e.dataTransfer.files;
    if (!files.length)
        return;

    var path = files[0].name;
    shoe.img = `src/assets/${path}`;
}

</script>

<template>
    <div class="form-add-shoe">
        <h1>Add Shoe</h1>
        <input id="shoeName" class="form-input" v-model="shoe.name"/>
        <input type="file" accept=".png, .webp," class="file" @change="onFileChange"/>
        <input id="shoeImage" class="form-input" v-model="shoe.img"/>
        <input id="shoeStartDate" type="date" class="form-input" v-model="shoe.startDate"/>
        <input id="shoeEstKm" type="number" class="form-input" v-model="shoe.estKm"/>
        <input id="shoeCurrentKm" type="number" class="form-input" v-model="shoe.currentKm"/>
        <button @click="$emit('addShoe', shoe)">Add Shoe</button>
    </div>
</template>

<style lang="scss" scoped>

</style>