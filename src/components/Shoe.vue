<script setup>
import { ref } from 'vue'

defineProps({
    shoe: {
        type: Object,
        required: true
    }
});

const flipped = ref(false);

</script>

<template>
    <div class="shoe" :class="{flipped: flipped}" @click="flipped = !flipped">
        <div class="shoe-front">
            <img class="img-shoe" :src="shoe.img"/>
        </div>
        <div class="shoe-back">
            <h1>{{shoe.name}}</h1>
            <p><span class="txt-start-date">Start Date:</span> {{shoe.startDate.toDateString()}}</p>
            <p>{{shoe.currentKm}}<meter min="0" :max="shoe.estKm" :value="shoe.currentKm"></meter>{{shoe.estKm}}</p>
        </div>
    </div>
</template>

<style lang="scss" scoped>

.shoe {
    position: relative;
    .shoe-front {
        background: #fff;
        backface-visibility: hidden;
        height: 100%;
        transform: rotateY(0deg);
        transform-style: preserve-3d;
        transition: transform var(--card-animation-speed) ease-in;
        z-index: 10;
    }

    .shoe-back {
        background: gray;
        backface-visibility: hidden;
        height: 100%;
        left: 0;
        position: absolute;
        top: 0;
        transform: rotateY(180deg);
        transform-style: preserve-3d;
        transition: transform var(--card-animation-speed) ease-in;
        width: 100%;
        z-index: 9;
    }

    &.flipped {
        .shoe-front {
            transform: rotateY(180deg);
            z-index: 9;
        }

        .shoe-back {
            transform: rotateY(0deg);
            z-index: 10;
        }
    }
}
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