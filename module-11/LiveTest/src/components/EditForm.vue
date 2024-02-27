<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['task']);
const emits = defineEmits(['submit', 'close']);

const editedTask = ref({ ...props.task });

const submitForm = () => {
  emits('submit', editedTask.value);
};

const closeForm = () => {
  emits('close');
};
</script>

<template>
  <div>
    <h2>
      Edit Task
    </h2>
    <form @submit.prevent="submitForm">
      <input class="" v-model="editedTask.name" type="text" placeholder="Task Name" />
      <input class="" v-model="editedTask.time" type="number" placeholder="Task Time" />
      <button class="btn" type="submit">Update Task</button>
    </form>
    <button class="btn" @click="closeForm">
      Close
    </button>
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