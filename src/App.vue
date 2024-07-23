<script setup>
import { useTaskStore } from "./stores/TaskStore";
import TaskDetails from "./components/TaskDetails.vue";
import TaskForm from "./components/TaskForm.vue";

import { ref } from "vue";
import { storeToRefs } from "pinia";

const filter = ref("all");

const taskStore = useTaskStore();

const { tasks, isLoading, favs, totalCount, favCount } = storeToRefs(taskStore);

// fetch tasks
taskStore.getTask();
</script>

<template>
  <main>
    <header>
      <img src="./assets//pinia.svg" alt="pinia-logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
      <button @click="taskStore.$reset">Reset state</button>
    </nav>

    <div class="loading" v-if="isLoading">Loading Tasks ...</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} favs left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<style></style>
