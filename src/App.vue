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
  const getTimeLabel = (time) => {
  return time === 1 ? 'Minute' : 'Minutes';
};
</script>

<template>
  <div class="shadow-md mt-12 flex flex-col p-5 mx-auto max-w-[400px] px-4 sm:px-6 lg:px-8 relative min-h-[300px]">
    <h1 class="text-3xl font-bold mb-5 text-center">
  Task List
</h1>
  
  <!-- Display Tasks -->
  <div class="flex gap-3 items-center mb-5 justify-between" v-for="(task, index) in tasks" :key="index">
    <span class="text-2xl font-bold">{{ task.name }} - {{ task.time }} {{ getTimeLabel(task.time) }}</span>
    <button class="text-red-500 px-0 py-0 mt-[5px] rounded-md" @click="removeTask(index)"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
</svg>
</button>
  </div>

  <!-- Add Task Button -->
  <button class="bg-blue-500 text-white px-3 py-2 rounded-md" @click="showAddTaskPopup">Add Task</button>

  <!-- Add Task Popup -->
  <div v-if="showPopup" class="absolute w-full h-full flex flex-col justify-center items-center bg-white top-0 left-0 p-5">
    <input class="mb-3 border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" v-model="newTask.name" placeholder="Task name">
    <input class="mb-3  border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" v-model.number="newTask.time" type="number" placeholder="Task time">
    <button class="bg-blue-500 text-white px-3 py-3 rounded-md w-full" @click="addTask">Add Task</button>
  </div>
  </div>


</template>

<style scoped>

</style>
