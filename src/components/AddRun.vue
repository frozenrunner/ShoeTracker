<script setup>
import { reactive } from 'vue'

const props = defineProps({
    isActive: {
        type: Boolean,
        required: true
    },
    activeShoe: {
        type: Object,
        required: true
    }
});

const emit = defineEmits(['addRun']);

const run = reactive({
    startDate: null,
    distance: 0
});

function emitAddRun() {
    emit('addRun', run, props.activeShoe)
    run.startDate = null;
    run.distance = 0;
}

</script>

<template>
        <div class="modal" :class="{'is-active': isActive }">
            <div class="modal-background" @click="$emit('closeAddRun')"></div>
            <div class="modal-content box">
                <label class="label" for="shoeName">Distance</label>
                <input id="shoeName" class="input form-input" v-model="run.distance" type="number"/>
                <label class="label" for="shoeRunDate">Run Date</label>
                <input id="shoeRunDate" class="input form-input shoe-run-date" type="date" v-model="run.startDate"/>
                <button class="button" @click="emitAddRun">Add Run</button>
            </div>
            <button class="modal-close is-medium" @click="$emit('closeAddRun')">X</button>
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

.input:last-of-type {
    margin-bottom: .625rem;
}

.dialog-close {
    position: absolute;
    right: 10px;
    top: 10px;    
}

</style>