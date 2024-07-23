<script setup>
import { useTaskStore } from '@/stores/TaskStore';
const useTask = useTaskStore()

const props = defineProps({
  task: Object,
});
</script>

<template>
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">
      <i class="material-icons" @click="useTask.deleteTask(task.id)">delete</i>
      <i class="material-icons" :class="{active: task.isFav}" @click="useTask.toggleFav(task.id)">favorite</i>
    </div>
  </div>
</template>
