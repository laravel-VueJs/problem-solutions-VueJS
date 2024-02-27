<script setup>
import { ref } from 'vue';
import EditForm from './EditForm.vue';

const tasks = ref([
  { name: 'Task 1', time: 30 },
  { name: 'Task 2', time: 40 },
  { name: 'Task 3', time: 60 },
  { name: 'Task 4', time: 45 },
  { name: 'Task 5', time: 50 },
]);


let isFormVisible = ref(false);
let editIndex = ref(null);

const openEditForm = (index) => {
  isFormVisible.value = true;
  editIndex.value = index;
};

const closeForm = () => {
  isFormVisible.value = false;
  editIndex.value = null;
};

const updateTask = (updatedTask) => {
  if (updatedTask.time === 0) {
    // Show an alert if the user tries to update time to 0 minutes
    alert("Time cannot be 0 minutes. Please enter a valid time.");
  } else {
    tasks.value[editIndex.value] = { ...updatedTask };
    isFormVisible.value = false;
    editIndex.value = null;
  }
};
</script>

<template>

  <div>
    <h1>Task List</h1>
    <div>
      <div class="grap" v-for="(task, index) in tasks" :key="index">
        <span>{{ task.name }} - {{ task.time }} {{ task.time > 1 ? "Minutes": "Minute" }}</span>
        <button class="btn text-white" @click="openEditForm(index)">
          Update
        </button>
      </div>
    </div>

    <EditForm
        v-if="isFormVisible"
        :task="tasks[editIndex]"
        @submit="updateTask"
        @close="closeForm"
    />
  </div>
</template>

<style scoped>
.grap{
  margin-bottom: 5px;
}
.text-white{
  color: white;
}
.btn {
  padding: 10px 20px;
  background-color: green;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>