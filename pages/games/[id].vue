<template>
  <div class=" bg-gray-900 mx-auto px-4 py-8">
    <!-- Back button -->
    <button @click="navigateTo('/games')" class="flex cursor-pointer items-center text-red-600 hover:text-red-800 mb-6">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd"
          d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z"
          clip-rule="evenodd" />
      </svg>
      Back to Explore
    </button>
    <!-- loading -->
    <div v-if="pending" class="flex justify-center items-center py-12">
      <Loading></Loading>
    </div>

    <!-- error -->
    <Error v-if="error"></Error>

    <!-- Game  details -->
    <div v-if="data && data.thumbnail" class="bg-gray-900 h-screen lg:h-auto  rounded-lg shadow-lg overflow-auto">
      <div class="md:flex">
        <div class="md:w-1/2 p-8 flex items-center justify-center ">
          <img :src="data.thumbnail" alt="image" class="max-h-80 object-contain" />
        </div>
        <div class="md:w-1/2 p-8">
          <div class="mb-2">
            <span class="text-white bg-red-800 text-xs font-medium px-2.5 py-0.5 rounded">
              {{ data.status }}
            </span>
          </div>
          <div class="mb-2">
            <span class="bg-white text-red-800 text-xs font-medium px-2.5 py-0.5 rounded">
              {{ data.genre }}
            </span>
          </div>
          <h1 class="text-2xl font-bold text-white mb-4">{{ data.title }}</h1>
          <p class="text-gray-100 mb-6">{{ data.short_description }}</p>
          <div class="w-full flex flex-col gap-2 lg:gap-1 lg:flex-row">
            <div class=" w-full lg:w-1/2">
              <span class="text-white bg-blue-800 text-xs font-medium px-2.5 py-0.5 rounded">
                {{ data.platform }}
              </span>
              <p class="text-gray-100 font-semibold">Publisher : {{ data.publisher }}</p>
              <p class="text-gray-100 font-semibold">Developer : {{ data.developer }}</p>
              <p class="text-gray-100 font-semibold">Release : {{ data.release_date }}</p>


            </div>
            <div class="w-full lg:w-1/2 py-4 rounded-2xl bg-white">
              <span class="text-red-800 text-xs font-medium px-2.5 py-0.5 ">
                Minimum System Requirements
              </span>
              <ul class="text-black text-xs px-2.5 py-0.5">
                <li>os: {{ data.minimum_system_requirements.os }}</li>
                <li>processor: {{ data.minimum_system_requirements.processor }}</li>
                <li>memory: {{ data.minimum_system_requirements.memory }}</li>
                <li>graphics: {{ data.minimum_system_requirements.graphics }}</li>
                <li>storage: {{ data.minimum_system_requirements.storage }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div class="w-full flex overflow-auto gap-2">
        <img class="w-1/3" v-for="picture in data.screenshots" :src="picture.image" :key="picture.id" alt="">
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const route = useRoute();
const config = useRuntimeConfig();
var id = route.params.id
var games;
const { data, pending, error, refresh } = await useAsyncData(
  'game',
  () => $fetch(`${config.public.apiBase}game?id=${id}`),
  {
    lazy: true,
    server: false,
  }
);
</script>

<style></style>