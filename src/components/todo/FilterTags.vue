<template>
    <button v-for="tag in tags"
            :key="tags.indexOf(tag)"
            :class="{activeTag: tag===currentTag}"
            @click="$emit('tagChanged', tag)"
    >
        {{tag}}
    </button>
</template>
<script setup>
defineProps({
    tags: {
        type: Array
    },
    currentTag: {
        type: String
    }
})
defineEmits(['tagChanged'])

</script>

<style scoped>
.activeTag {
    background: blue;
    color: yellow;
}
</style>