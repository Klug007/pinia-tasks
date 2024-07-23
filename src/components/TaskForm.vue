<script setup>
import { ref } from "vue";
import {useTaskStore} from '../stores/TaskStore.js'

const taskStore = useTaskStore()

const newTask = ref("");


const handleSubmit = () => {
  if(newTask.value.trim() === '') return 

  taskStore.addTask({
    title: newTask.value,
    isFav: false,
    id: (Math.floor(Math.random() * 1000000)).toString()
  })

  newTask.value = ''
}

</script>

<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" placeholder="I need to..." v-model="newTask" />
    <button>Add</button>
  </form>
</template>
