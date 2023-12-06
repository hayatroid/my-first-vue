<script setup lang="ts">
import { computed, ref } from 'vue'

interface Task {
    finished: boolean
    name: string,
}

const tasks = ref<Task[]>([])
const finishedTasks = computed(() => tasks.value.filter((task) => task.finished))
const notFinishedTasks = computed(() => tasks.value.filter((task) => !task.finished))

const newTaskName = ref('')

const addTask = () => {
    if (newTaskName.value !== '' && !tasks.value.some((task) => task.name === newTaskName.value)) {
        tasks.value.push({finished: false, name: newTaskName.value})
    }
    newTaskName.value = ''
}
</script>

<template>
    <div>TodoList</div>
    <div>完了済みタスク一覧</div>
    <ul>
        <li v-for="task in finishedTasks" :key="task.name">
            <div>{{ task.name }}</div>
        </li>
    </ul>
    <div>未完タスク一覧</div>
    <ul>
        <li v-for="task in notFinishedTasks" :key="task.name">
            <div>{{ task.name }}</div>
            <button @click="task.finished = true">完了する</button>
        </li>
    </ul>
    <div>
        <label>
            タスク名
            <input type="text" v-model="newTaskName" />
        </label>
        <button @click="addTask">追加</button>
    </div>
</template>

<style>
</style>