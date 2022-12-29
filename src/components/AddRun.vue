<script setup>
import { reactive } from 'vue'

defineProps({
    isActive: {
        type: Boolean,
        required: true
    }
});

const run = reactive({
    startDate: null,
    distance: 0
});

</script>

<template>
        <div class="modal" :class="{'is-active': isActive }">
            <div class="modal-background" @click="$emit('closeAddRun')"></div>
            <div class="modal-content box">
                <label class="label" for="shoeName">Distance</label>
                <input id="shoeName" class="input form-input" v-model="run.distance" type="number"/>
                <label class="label" for="shoeRunDate">Run Date</label>
                <input id="shoeRunDate" class="input form-input" type="date" v-model="run.startDate"/>
                <button class="button" @click="$emit('addRun', run)">Add Run</button>
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

.dialog-close {
    position: absolute;
    right: 10px;
    top: 10px;    
}
</style>