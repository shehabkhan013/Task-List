<script setup>
import { ref } from 'vue';

const tasks = ref([
  { name: 'Task 1', time: 60 },
  { name: 'Task 2', time: 75 },
]);

const showPopup = ref(false);
const newTask = ref({ name: '', time: 0 });

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const showAddTaskPopup = () => {
  showPopup.value = true;
};

const addTask = () => {
  if (newTask.value.name && newTask.value.time > 0) {
    tasks.value.push({ ...newTask.value });
    newTask.value = { name: '', time: 0 };
    showPopup.value = false;
  } else {
    alert('Please provide a valid task name and time.');
  }
};
</script>

<template>
  <div class="shadow-md mt-12 flex flex-col p-5 mx-auto max-w-[400px] px-4 sm:px-6 lg:px-8 relative min-h-[300px]">
    <h1 class="text-3xl font-bold mb-5 text-center">
  Task List
</h1>
  
  <!-- Display Tasks -->
  <div class="flex gap-3 items-center mb-5 justify-between" v-for="(task, index) in tasks" :key="index">
    <span class="text-2xl font-bold">{{ task.name }} - {{ task.time }} minutes</span>
    <button class="bg-red-500 text-white px-3 py-1 rounded-md" @click="removeTask(index)">Remove</button>
  </div>

  <!-- Add Task Button -->
  <button class="bg-blue-500 text-white px-3 py-1 rounded-md" @click="showAddTaskPopup">Add Task</button>

  <!-- Add Task Popup -->
  <div v-if="showPopup" class="absolute w-full h-full flex flex-col justify-center items-center bg-white top-0 left-0 p-5">
    <input class="mb-3 border border-[px] w-full h-[50px] px-4" v-model="newTask.name" placeholder="Task name">
    <input class="mb-3 border border-[px] w-full h-[50px] px-4" v-model.number="newTask.time" type="number" placeholder="Task time">
    <button class="bg-blue-500 text-white px-3 py-1 rounded-md w-full" @click="addTask">Add Task</button>
  </div>
  </div>


</template>

<style scoped>

</style>
