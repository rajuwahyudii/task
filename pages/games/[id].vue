<template>
  <div class="container bg-gray-900 mx-auto px-4 py-8">
    <!-- Back button -->
    <button @click="navigateTo('/games')" class="flex items-center text-red-600 hover:text-red-800 mb-6">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd"
          d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z"
          clip-rule="evenodd" />
      </svg>
      Back to Explore
    </button>
    <!-- loading -->
    <div class="flex justify-center items-center py-12">
      <Loading></Loading>
    </div>

    <!-- error -->
    <Error></Error>

    <!-- Game  details -->
    <div class="bg-gray-900 h-screen rounded-lg shadow-lg overflow-hidden">
      <div class="md:flex">
        <div class="md:w-1/2 p-8 flex items-center justify-center ">
          <img src="https://mmobomb.com/g/9/thumbnail.jpg" alt="image" class="max-h-80 object-contain" />
        </div>
        <div class="md:w-1/2 p-8">
          <div class="mb-2">
            <span class="bg-white text-red-800 text-xs font-medium px-2.5 py-0.5 rounded">
              category
            </span>
          </div>
          <h1 class="text-2xl font-bold text-white mb-4">title {{ id }}</h1>
          <p class="text-gray-100 mb-6">description</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const route = useRoute();
var id = route.params.id
</script>

<style></style>