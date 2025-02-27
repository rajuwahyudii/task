<template>
  <div class="min-h-screen bg-gray-900 text-white">
    <Navbar />
    <div class="w-full flex justify-between">
      <h1 class="text-3xl font-bold text-left  m-8 text-white">Explorer Game</h1>
      <button class="text-white w-4 mr-10 cursor-pointer" @click="openAddModal">
        <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 448 512">
          <path d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32l0 144L48 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l144 0 0 144c0 17.7 14.3 32 32 32s32-14.3 32-32l0-144 144 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-144 0 0-144z"/>
        </svg>
      </button>
    </div>
    <AddGames 
    :is-open="isModalOpen" 
      @close="closeModal"
    />
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 p-2">
      <!-- loading -->
      <div v-if="pending" class="flex justify-center items-center py-12">
        <Loading></Loading>
      </div>
      <!-- error -->
      <Error v-if="error"></Error>
      <RouterLink v-if="data && data.length > 0" v-for="game in data" :key="game.id" :to="`/games/${game.id}`">
        <Card :data="game">
        </Card>
      </RouterLink>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import AddGames from '~/components/add-games.vue';
const config = useRuntimeConfig();
const { data, pending, error, refresh } = await useAsyncData(
  'pc-games',
  () => $fetch(`${config.public.apiBase}games?platform=pc`),
  {
    lazy: true,
    server: false,
  }
);
const isModalOpen = ref(false);
function openAddModal() {
  isModalOpen.value = true;
}
function closeModal() {
  isModalOpen.value = false;
}

if (data.value && data.value.length > 0) {
  console.log(data.value[0].id);
}




</script>