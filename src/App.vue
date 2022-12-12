<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Shoe from './components/Shoe.vue'
</script>

<script>
export default {
  data() {
    return {
      shoes: [{
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
      }]
    }
  }
}
</script>

<template>
  <main>
    <Shoe v-for="shoe in shoes" :shoe="shoe"/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
