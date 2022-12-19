<script setup>
import { ref } from 'vue'
import Shoe from './components/Shoe.vue'
import AddShoe from './components/AddShoe.vue'

const showAddShoe = ref(false);

const shoes = ref([{
        name: "Brooks Ghost 14",
        img: "src/assets/brooks-ghost-14-grey.jpg",
        startDate: new Date("2022-01-01 00:00:00"),
        estKm: 1000,
        currentKm: 230
      },
      {
        name: "Nike Pegasus 39",
        img: "src/assets/nike-pegasus-39.jpg",
        startDate: new Date("2022-04-01 00:00:00"),
        estKm: 1500,
        currentKm: 130
      },
      {
        name: "Brooks Launch 9",
        img: "src/assets/brooks-launch-9-boston.webp",
        startDate: new Date("2022-05-01 00:00:00"),
        estKm: 800,
        currentKm: 630
      }]);

function addShoe(newShoe) {
  shoes.value.push({
    name: newShoe.name,
    img: newShoe.img,
    startDate: new Date(`${newShoe.startDate} 00:00:00`),
    estKm: newShoe.estKm,
    currentKm: newShoe.currentKm
  })
}

function toggleAddShoe() {
  showAddShoe.value = !showAddShoe.value;
}

function closeAddShoe() {
  showAddShoe.value = false;
}
</script>

<template>
  <div class="grid-shoe">
    <Shoe v-for="shoe in shoes" :shoe="shoe"/>
  </div>
  <button class="button-toggle-add-shoe" @click="toggleAddShoe">Add Shoe</button>
  <AddShoe v-show="showAddShoe" :shoes="shoes" @add-shoe="addShoe" @close-add-shoe="closeAddShoe"/>
</template>

<style lang="scss" scoped>
  .grid-shoe {
    display: grid;
    column-gap: 1rem;
    grid-template-columns: 1fr 1fr 1fr;
    padding: 0 2rem;
    row-gap: 1rem;
  }
  .button-toggle-add-shoe {
    left: 0;
    position: absolute;
    top: 0;
  }
</style>
