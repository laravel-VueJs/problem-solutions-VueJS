<script setup>
import { reactive, ref } from 'vue';

const isLoading = ref(true);
const quote = reactive({
  id: "",
  quote: "",
  anime: "",
  character: ""
});

const fetchData = async () => {
  try {
    const response = await fetch('https://animechan.xyz/api/random');
    const data = await response.json();
    quote.id = data.id;
    quote.quote = data.quote;
    quote.anime = data.anime;
    quote.character = data.character;
    isLoading.value = false;
  } catch (e) {
    alert('Data dose not loading properly', e);
    isLoading.value = false;
  }
};
fetchData();
</script>

<template>
  <div class="shadow-2xl p-5 rounded">
    <h4 class="text-xl font-bold text-center">Fetch API</h4>
    <hr class="mb-3">
    <!-- Conditional rendering based on loading state -->
    <div v-if="isLoading">
      <!-- Loader -->
      <div class="text-center">Loading...</div>
    </div>
    <div v-else-if="quote.id">
      <!-- Quote content -->
      <ul class="d-flex flex-col gap-5">
        <li class="text-left text-1xl flex gap-2">
          <span class="font-bold capitalize">ID:</span> {{ quote.id }}
        </li>
        <li class="text-left text-1xl flex gap-2 mt-2">
          <span class="font-bold capitalize">quote:</span> {{ quote.quote }}
        </li>
        <li class="text-left text-1xl flex gap-2 mt-2">
          <span class="font-bold capitalize">anime:</span> {{ quote.anime }}
        </li>
        <li class="text-left text-1xl flex gap-2 mt-2">
          <span class="font-bold capitalize">character:</span> {{ quote.character }}
        </li>
      </ul>
    </div>
    <div v-else="quote.id" class="text-center font-bold text-red-500">
      Not Found
    </div>
  </div>
</template>
