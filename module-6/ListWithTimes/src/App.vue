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

const closeBtn = () => {
  showPopup.value = false;
}

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
  <div class="relative">
    <div class="rounded-2xl w-[400px] border border-blue-100 bg-white p-4 shadow-lg sm:p-6 lg:p-8mt-12 flex flex-col mx-auto min-w-[400px] px-4 mb-5 sm:px-6 lg:px-8 min-h-[300px]">
      <h1 class="text-3xl font-bold mb-5 text-center">
        Task List
      </h1>

      <!-- Display Tasks -->
      <div class="flex gap-3 items-center mb-5 justify-between" v-for="(task, index) in tasks" :key="index">
        <span class="text-xl font-bold">{{ task.name }} - {{task.time}} <span v-text="task.time<=1?'Minute':'Minutes'"></span></span>
        <button class="btn bg-red-600 text-white px-2 py-1 mt-[5px]" @click="removeTask(index)">
          Remove
        </button>
      </div>
    </div>

    <!-- Add Task Button -->
    <button class="bg-blue-500 text-white px-3 py-2 rounded-md" @click="showAddTaskPopup">Add Task</button>

    <!-- Add Task Popup -->
    <div v-if="showPopup" class="absolute top-0 left-0 rounded-2xl w-[400px] border border-blue-100 bg-white p-4 shadow-lg sm:p-6 lg:p-8">
      <div class="flex items-center justify-between">
        <p class="font-medium sm:text-lg">Add New Task</p>
        <h3 @click="closeBtn()" class="btn bg-red-600 text-white px-2 py-1 rounded cursor-pointer">Close</h3>
      </div>

      <div class="mt-4">
        <input class="mb-3 rounded border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" v-model="newTask.name" placeholder="Task name">
        <input class="mb-3 rounded border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" @keypress.enter="addTask()" v-model.number="newTask.time" type="number" placeholder="Task time">
      </div>

      <div class="mt-6 sm:flex sm:gap-4">
        <button class="bg-blue-500 text-white px-3 py-3 rounded-md w-full" @click="addTask">Add Task</button>
      </div>
    </div>

  </div>

</template>

<style scoped>

</style>