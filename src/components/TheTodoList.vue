<template>
    <NewTask @addTask="handleAddTask($event)"/>
    <TodoList
        :tasks="todoList"
        title="Todo List"
    >
    </TodoList>
    <TodoList
        :tasks="completedList"
        title="Completed"
        toggleable
    >
    </TodoList>
</template>

<script setup>
    import {computed, ref} from "vue";
    import TodoList from "@/components/todo/TodoList.vue";
    import NewTask from "@/components/todo/NewTask.vue";

    const allList = ref([
        {id:1, name: 'first task', complete: false, tag: 'bla'},
        {id:2, name: '2nd task', complete: true, tag: 'bla'},
        {id:3, name: '3rd task', complete: false, tag: 'blabla'},

    ]);

    const completedList = computed(() => {
        return allList.value.filter(task => task.complete)
    })
    const todoList = computed(() => {
        return allList.value.filter(task => !task.complete)
    })

    function handleAddTask(task) {
        allList.value.push({
            id: allList.value.length + 1,
            name: task,
            completed: false,
            tag: 'new'
        });
    }
</script>