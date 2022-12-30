<script setup>
import { ref } from 'vue'
import Shoe from './components/Shoe.vue'
import AddShoe from './components/AddShoe.vue'
import AddRun from './components/AddRun.vue'
import brooksGhost from './assets/brooks-ghost-14-grey.jpg'
import nikePegasus from './assets/nike-pegasus-39.jpg'
import brooksLaunch from './assets/brooks-launch-9-boston.webp'
import dsTrainer from './assets/asics-ds-trainer-26.webp'
import metaSpeed from './assets/asics-metaspeed-sky.webp'
import novaBlast from './assets/asics-novablast-3.webp'

const showAddShoe = ref(false);
const showAddRun = ref(false);
const activeShoe = ref(null);

const shoes = ref([{
        name: "Brooks Ghost 14",
        img: brooksGhost,
        startDate: new Date("2022-01-01 00:00:00"),
        estKm: 1000,
        blurb: "The Ghost 14 is a dependable workhorse that has the perfect balance of long-distance cushioning and ride stability. It excels on long-distances and steady-paced runs.",
        runHistory: [
          {
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 25
          },
          {
            date: formatDate(new Date("2022-02-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-02-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-02-10 00:00:00")),
            distance: 25
          },
          {
            date: formatDate(new Date("2022-03-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-03-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-03-10 00:00:00")),
            distance: 25
          },
          {
            date: formatDate(new Date("2022-04-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-04-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-04-10 00:00:00")),
            distance: 25
          },
          {
            date: formatDate(new Date("2022-05-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-05-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-05-10 00:00:00")),
            distance: 25
          }
        ]
      },
      {
        name: "Nike Pegasus 39",
        img: nikePegasus,
        startDate: new Date("2022-04-01 00:00:00"),
        estKm: 1500,
        blurb: "The Nike Air Zoom Pegasus 39 is a comfortable, mid-range daily trainer designed to be durable.",
        runHistory: [{
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 50
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 75
          }]
      },
      {
        name: "Brooks Launch 9",
        img: brooksLaunch,
        startDate: new Date("2022-05-01 00:00:00"),
        estKm: 800,
        blurb: "The Brooks Launch 9 will tick most of your boxes as a good all round running shoe.",
        runHistory: [{
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 110
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 120
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 125
          }]
      },
      {
        name: "Asics Gel-DS Trainer 26",
        img: dsTrainer,
        startDate: new Date("2022-06-01 00:00:00"),
        estKm: 1000,
        blurb: "The ASICS Gel-DS Trainer 26 is a top notch short-to-mid distance shoe geared toward speed,",
        runHistory: [{
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 60
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 70
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 85
          }]
      },
      {
        name: "Asics MetaSpeed Sky",
        img: metaSpeed,
        startDate: new Date("2022-07-01 00:00:00"),
        estKm: 500,
        blurb: "The Asics Metaspeed Sky is a rocket. Its stiff carbon plate combined with its high toe-spring rocker results in one of the fastest-feeling super shoes that money can buy.",
        runHistory: [{
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 10
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 15
          }]
      },
      {
        name: "Asics NovaBlast 3",
        img: novaBlast,
        startDate: new Date("2022-08-01 00:00:00"),
        estKm: 1200,
        blurb: "The Novablast 3 is a very good long run shoe and just eats up miles.",
        runHistory: [{
            date: formatDate(new Date("2022-01-01 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-01-05 00:00:00")),
            distance: 20
          },
          {
            date: formatDate(new Date("2022-01-10 00:00:00")),
            distance: 25
          }]
      }]);

function formatDate(date) {
  return date.toISOString().split('T')[0];
}

function addShoe(newShoe) {
  shoes.value.push({
    name: newShoe.name,
    img: newShoe.img,
    startDate: new Date(`${newShoe.startDate} 00:00:00`),
    estKm: newShoe.estKm,
    blurb: newShoe.blurb
  });
  closeAddShoe();
}

function toggleAddShoe() {
  document.documentElement.classList.toggle("is-clipped");
  showAddShoe.value = !showAddShoe.value;
}

function closeAddShoe() {
  document.documentElement.classList.remove("is-clipped");
  showAddShoe.value = false;
}

function addRun(run, shoe) {
  shoe.runHistory.push({
    date: run.startDate,
    distance: run.distance
  });
  closeAddRun();
}

function toggleAddRun(event, shoe) {
  document.documentElement.classList.toggle("is-clipped");
  showAddRun.value = !showAddRun.value;
  activeShoe.value = shoe;
  event.stopPropagation();
}

function closeAddRun() {
  document.documentElement.classList.remove("is-clipped");
  showAddRun.value = false;
}
</script>

<template>
  <main>
    <div id="instructions" class="instructions">
      <h1>Instructions</h1>
      <p>Click each shoe to flip the card and see the run history</p>
      <p>Shoes can be added using the "Add Shoe" button</p>
      <p>This is an experiment to get familiar with Vue3 after having spent many years working in Vue2</p>
    </div>
    <button class="button button-toggle-add-shoe" @click="toggleAddShoe">Add Shoe</button>
    <Shoe v-for="shoe in shoes" :shoe="shoe" @toggle-add-run="toggleAddRun" />
    <AddShoe :isActive="showAddShoe" @add-shoe="addShoe" @close-add-shoe="closeAddShoe" />
    <AddRun :isActive="showAddRun" :activeShoe="activeShoe" @add-run="addRun" @close-add-run="closeAddRun"/>
  </main>
</template>

<style lang="scss" scoped>
  main {
    display: grid;
    grid-gap: 8px;
    grid-template-columns: repeat(4, minmax(70px, 1fr));

    @media (min-width: 768px) {
      grid-template-columns: repeat(6, 1fr);
    }

    @media (min-width: 1024px) {
      grid-template-columns: repeat(8, 1fr);
    }
  }

  .instructions {
    grid-column: 1 / -2;
  }

  .button-toggle-add-shoe {
    align-self: center;
    grid-column: -2 / -1;
  }
</style>
