<script setup>
defineProps({
    shoe: {
        type: Object,
        required: true
    }
});
</script>

<template>
    <div class="shoe">
        <h1>{{shoe.name}}</h1>
        <img class="img-shoe" :src="shoe.img"/>
        <p><span class="txt-start-date">Start Date:</span> {{shoe.startDate.toDateString()}}</p>
        <p>{{shoe.currentKm}}<meter min="0" :max="shoe.estKm" :value="shoe.currentKm"></meter>{{shoe.estKm}}</p>
    </div>
</template>

<style lang="scss" scoped>
.img-shoe {
    width: 200px;

    @media (min-width: 1024px) {
        width: 400px;
    }
}

.txt-start-date {
    font-weight: 700;
}
</style>