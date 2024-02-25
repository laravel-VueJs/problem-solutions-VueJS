<script setup>
import { ref } from 'vue';

const num1 = ref(null);
const num2 = ref(null);
const operator = ref('+');
const result = ref(null);

const calculate = () => {
  switch (operator.value) {
    case '+':
      result.value = num1.value + num2.value;
      break;
    case '-':
      result.value = num1.value - num2.value;
      break;
    case '*':
      result.value = num1.value * num2.value;
      break;
    case '/':
      result.value = num1.value / num2.value;
      break;
  }
};
</script>

<template>
  <div class="flex flex-col items-center justify-center gap-4 shadow-2xl p-5 rounded">
    <h4 class="text-xl font-bold text-center border-b">Calculator</h4>
    <div class="flex flex-col gap-2 w-full items-start">
      <label for="num1" class="cursor-pointer block text-sm font-medium text-gray-900 dark:text-white">Input number</label>
      <input type="number" name="price" id="num1" class="block w-full rounded-md border-0 py-2 px-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-blue-500 focus:border-blue-500 sm:text-sm sm:leading-6" placeholder="0.00" v-model="num1">
    </div>

    <div class="flex flex-col gap-2 w-full items-start">
      <label for="num2" class="cursor-pointer block text-sm font-medium text-gray-900 dark:text-white">Input number</label>
      <input type="number" name="price" id="num2" class="block w-full rounded-md border-0 py-2 px-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-blue-500 focus:border-blue-500 sm:text-sm sm:leading-6" placeholder="0.00" v-model="num2">
    </div>

    <div class="flex flex-col gap-2 w-full items-start">
      <label for="operations" class="cursor-pointer block text-sm font-medium text-gray-900 dark:text-white">Operations</label>
      <select id="operations" v-model="operator" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
        <option value="+">Plus</option>
        <option value="-">Minus</option>
        <option value="*">Multiply</option>
        <option value="/">Divide</option>
      </select>
    </div>

    <div v-if="result !== null" class="text-1xl font-bold">Result: {{ result }}</div>

    <template v-if="(!num1 >= 1 || !num2 >= 1)">
      <button  @click="calculate" disabled class="bg-gray-300 hover:bg-green-800 text-black hover:text-white font-bold py-2 px-4 rounded w-full uppercase">Please Input Number</button>
    </template>
    <div v-else>
      <button  @click="calculate" class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded w-full uppercase">Calculate</button>
    </div>

  </div>
</template>

<style scoped>

</style>