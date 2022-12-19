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
    var files = e.target.files || e.dataTransfer.files;
    if (!files.length)
        return;

    var path = files[0].name;
    shoe.img = `src/assets/${path}`;
}

</script>

<template>
    <div class="container-form">
        <div class="form-add-shoe">
            <h1>Add Shoe</h1>
            <label for="shoeName">Shoe Name</label>
            <input id="shoeName" class="form-input" v-model="shoe.name"/>
            <label for="file">Shoe Image</label>
            <input type="file" accept=".png, .webp, .jpg" class="file" @change="onFileChange"/>
            <label for="shoeStartDate">Start Date</label>
            <input id="shoeStartDate" type="date" class="form-input" v-model="shoe.startDate"/>
            <label for="shoeEstKm">Estimated Kilometers</label>
            <input id="shoeEstKm" type="number" class="form-input" v-model="shoe.estKm"/>
            <label for="shoeCurrentKm">Current Kilometers</label>
            <input id="shoeCurrentKm" type="number" class="form-input" v-model="shoe.currentKm"/>
            <button @click="$emit('addShoe', shoe)">Add Shoe</button>
            <button class="dialog-close" @click="$emit('closeAddShoe')">X</button>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.container-form {
    align-items: center;
    background: rgba(0,0,0,.4);
    color: var(--color-dialog-text);
    display: flex;
    height: 100%;
    justify-content: center;
    left: 0;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 99;
}
.form-add-shoe {
    background: #fff;
    display: flex;
    flex-flow: column nowrap;
    padding: 10px;
    position: fixed;
}

.dialog-close {
    position: absolute;
    right: 10px;
    top: 10px;    
}
</style>