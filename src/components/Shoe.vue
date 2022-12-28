<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
    shoe: {
        type: Object,
        required: true
    }
});

const flipped = ref(false);

const totalDistance = computed(() => {
    let total = 0;
    for (let i = 0, len = props.shoe.runHistory.length; i<len; i++) {
        total += props.shoe.runHistory[i].distance;
    }
    return total;
})
</script>

<template>
    <div class="shoe" :class="{flipped: flipped}" @click="flipped = !flipped">
        <div class="box shoe-front">
            <div class="shoe-inner">
                <h2 class="content shoe-name">{{ shoe.name }}</h2>
                <img class="shoe-img" :src="shoe.img"/>
                <p class="content is-small shoe-blurb">{{ shoe.blurb }}</p>
                <p><span class="txt-start-date">Start Date:</span> {{shoe.startDate.toISOString().split('T')[0]}}</p>
                <div class="progress-container"><span>{{totalDistance}}</span><progress class="progress shoe-progress" :max="shoe.estKm" :value="totalDistance"></progress><span>{{shoe.estKm}}</span></div>
            </div>
        </div>
        <div class="box shoe-back">
            <h2 class="title is-5">History</h2>
            <p v-for="run in shoe.runHistory"><span>{{ run.date.toISOString().split('T')[0] }}</span>:{{ run.distance }}</p>
        </div>
    </div>
</template>

<style lang="scss" scoped>

.shoe {
    grid-column: span 2;
    position: relative;

    .shoe-inner {
        display: flex;
        flex-flow: column nowrap;
        height: 100%;
    }

    .shoe-front {
        backface-visibility: hidden;
        background-color: var(--teal-1);
        background-image: linear-gradient(0deg, var(--teal-1) 0%, var(--teal-2) 100%);
        border: 1px solid var(--teal-3);
        height: 100%;
        padding: 0 .625rem .625rem;
        transform: rotateY(0deg);
        transform-style: preserve-3d;
        transition: transform var(--card-animation-speed) ease-in;
        z-index: 10;

        .shoe-name {
            border-radius: 5px;
            font-weight: 700;
            padding: .5rem;
            margin: 0;
        }

        .shoe-img {
            align-self: center;
            margin: 0 0 1rem;
            max-height: 107px;
            width: 200px;

            @media (min-width: 768px) {
                max-height: 173px;
            }

            @media (min-width: 1024px) {
                margin: 0 0 1rem;
                width: 400px;
            }
        }

        .shoe-blurb {
            background: var(--blue-2);
            border: 1px solid var(--blue-4);
            border-radius: 5px;
            color: #fff;
            flex: 1 1 auto;
            padding: .5rem;
        }
    }

    .shoe-back {
        backface-visibility: hidden;
        background-color: #f2f5fb;
        background-image: linear-gradient(0deg, #f2f5fb 0%, #97D9E1 100%);
        border: 1px solid var(--teal-3);
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

    .progress-container {
        align-items: center;
        display: flex;
        flex-flow: row nowrap;

        span {
            &:first-child {
                margin: 0 10px 0 0;
            }

            &:last-child {
                margin: 0 0 0 10px;
            }
        }

        .shoe-progress {
            background-color: var(--teal-3);
            display: inline;
            margin: 0;
            &::-moz-progress-bar {
                background-color: var(--teal-5);
            }
            &::-webkit-progress-value {
                background-color: var(--teal-5);
            }
        }
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

.txt-start-date {
    font-weight: 700;
}
</style>