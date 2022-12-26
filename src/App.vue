<script setup>
import { ref } from 'vue'
import Shoe from './components/Shoe.vue'
import AddShoe from './components/AddShoe.vue'
import brooksGhost from './assets/brooks-ghost-14-grey.jpg'
import nikePegasus from './assets/nike-pegasus-39.jpg'
import brooksLaunch from './assets/brooks-launch-9-boston.webp'
import dsTrainer from './assets/asics-ds-trainer-26.webp'
import metaSpeed from './assets/asics-metaspeed-sky.webp'
import novaBlast from './assets/asics-novablast-3.webp'

const showAddShoe = ref(false);

const shoes = ref([{
        name: "Brooks Ghost 14",
        img: brooksGhost,
        startDate: new Date("2022-01-01 00:00:00"),
        estKm: 1000,
        currentKm: 230,
        blurb: "The Ghost 14 is a dependable workhorse that has the perfect balance of long-distance cushioning and ride stability. It excels on long-distances and steady-paced runs."
      },
      {
        name: "Nike Pegasus 39",
        img: nikePegasus,
        startDate: new Date("2022-04-01 00:00:00"),
        estKm: 1500,
        currentKm: 130,
        blurb: "The Nike Air Zoom Pegasus 39 is a comfortable, mid-range daily trainer designed to be durable."
      },
      {
        name: "Brooks Launch 9",
        img: brooksLaunch,
        startDate: new Date("2022-05-01 00:00:00"),
        estKm: 800,
        currentKm: 630,
        blurb: "The Brooks Launch 9 will tick most of your boxes as a good all round running shoe."
      },
      {
        name: "Asics Gel-DS Trainer 26",
        img: dsTrainer,
        startDate: new Date("2022-06-01 00:00:00"),
        estKm: 1000,
        currentKm: 330,
        blurb: "The ASICS Gel-DS Trainer 26 is a top notch short-to-mid distance shoe geared toward speed,"
      },
      {
        name: "Asics MetaSpeed Sky",
        img: metaSpeed,
        startDate: new Date("2022-07-01 00:00:00"),
        estKm: 500,
        currentKm: 100,
        blurb: "The Asics Metaspeed Sky is a rocket. Its stiff carbon plate combined with its high toe-spring rocker results in one of the fastest-feeling super shoes that money can buy."
      },
      {
        name: "Asics NovaBlast 3",
        img: novaBlast,
        startDate: new Date("2022-08-01 00:00:00"),
        estKm: 1200,
        currentKm: 400,
        blurb: "The Novablast 3 is a very good long run shoe and just eats up miles."
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
  <div id="instructions" class="instructions">
    <h1>Instructions</h1>
    <p>Click each shoe to flip the card and see the stats!</p>
    <p>Shoes can be added using the "Add Shoe" button</p>
  </div>
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
    grid-template-columns: 1fr;
    padding: 0 2rem;
    row-gap: 1rem;

    @media (min-width: 1024px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
  .button-toggle-add-shoe {
    left: 0;
    position: absolute;
    top: 0;
  }
</style>
