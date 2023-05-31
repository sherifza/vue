<template>
    <section v-show="filteredTasks.length && !hideMe">
        <h2 > {{title}} ( {{ filteredTasks.length }} )<span @click="hideMe = true" v-show="toggleable">&times;</span></h2>
            <FilterTags
                    :tags="tags"
                    :currentTag="currentTag"
                    @tagChanged="($event)=>{currentTag=$event}"
            >
            </FilterTags>
        <ul>
            <ATask v-for="task in filteredTasks"
                :key="task.id"
                :task="task"
            ></ATask>
        </ul>
    </section>
</template>
<script setup>
import ATask from "@/components/todo/ATask.vue";
import {computed, ref, getCurrentInstance} from "vue";
import FilterTags from "@/components/todo/FilterTags.vue";

let hideMe=ref(false);
let currentTag=ref('all');

const props = getCurrentInstance().props;

const filteredTasks = computed(() => {
    if (currentTag.value === 'all') {
        return props.tasks;
    }
    return props.tasks.filter(task => task.tag === currentTag.value)
})
const tags = computed(() => {
    return ['all', ...new Set(props.tasks.map(task=>task.tag))];
})

defineProps({
    tasks: {
        type: Array,
        required: true
    },
    title: {
        type: String,
        required: true
    },
    toggleable: {
        type: Boolean,
        default: false
    }
})

</script>