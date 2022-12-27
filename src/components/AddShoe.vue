<script setup>
import { reactive } from 'vue'

defineProps({
    isActive: {
        type: Boolean,
        required: true
    }
});

const shoe = reactive({
    name: "",
    img: "",
    startDate: null,
    estKm: 0,
    currentKm: 0,
    blurb: ""
});

function onFileChange(e) {
    const files = e.target.files || e.dataTransfer.files;
    if (!files.length) {
        return;
    }

    getImgBase64(files[0]);
}

function getImgBase64(file) {
    var reader = new FileReader();

    reader.readAsDataURL(file);
    reader.onload = () => {
        shoe.img = reader.result;
    };
    reader.onerror = (error) => {
        console.log('Error: ', error);
    };
}

</script>

<template>
        <div class="modal" :class="{'is-active': isActive }">
            <div class="modal-background" @click="$emit('closeAddShoe')"></div>
            <div class="modal-content box">
                <label class="label" for="shoeName">Shoe Name</label>
                <input id="shoeName" class="input form-input" v-model="shoe.name" type="text"/>
                <label class="label" for="file">Image</label>
                <input accept=".png, .webp, .jpg" class="input file" type="file" @change="onFileChange"/>
                <label class="label" for="shoeStartDate">Start Date</label>
                <input id="shoeStartDate" class="input form-input" type="date" v-model="shoe.startDate"/>
                <label class="label" for="shoeEstKm">Estimated Kilometers</label>
                <input id="shoeEstKm" class="input orm-input" type="number" v-model="shoe.estKm"/>
                <label class="label" for="shoeCurrentKm">Current Kilometers</label>
                <input id="shoeCurrentKm" class="input form-input" type="number"  v-model="shoe.currentKm"/>
                <label class="label" for="shoeBlurb">Blurb</label>
                <textarea id="shoeBlurb" class="textarea" v-model="shoe.blurb"></textarea>
                <button class="button" @click="$emit('addShoe', shoe)">Add Shoe</button>
            </div>
            <button class="modal-close is-medium" @click="$emit('closeAddShoe')">X</button>
        </div>
</template>

<style lang="scss" scoped>
.textarea {
    margin-bottom: .5rem;
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