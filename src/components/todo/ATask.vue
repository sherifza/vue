<template>
    <li>
        <label>{{ task.name }}</label>
        <input type="checkbox" v-model="task.complete">
    </li>
</template>

<script setup>
defineProps({
    task: {
        type: Object,
        required: true
    }
})


</script>