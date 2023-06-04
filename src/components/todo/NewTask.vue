<template>
    <form @submit.prevent="emitNewTask">
        <input placeholder="new task" v-model="newTask">
        <button type="submit">Add</button>
    </form>
</template>

<script setup>
import { defineEmits, ref } from 'vue';

const emit = defineEmits(['addTask']);

const newTask = ref('');

const emitNewTask = () => {
    emit('addTask', newTask.value);
    newTask.value = '';
};
</script>