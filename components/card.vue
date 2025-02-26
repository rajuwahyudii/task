<template>
  <!-- <div v-for="item in filteredItems" :key="item.id" @click="selectItem(item)" -->
  <div class="bg-white rounded-lg shadow-md p-4 cursor-pointer transform transition hover:scale-105">
    <div class="w-full flex mb-4">
      <img class="mx-auto" src="https://mmobomb.com/g/9/thumbnail.jpg" alt="thumbnail">
    </div>
    <h3 class="font-semibold text-black text-lg mb-2">World</h3>
    <!-- <p class="text-gray-600 text-sm mb-4">{{ item.description }}</p> -->
    <p class="text-gray-600 text-sm ">Publisher : Level Invinite</p>
    <p class="text-gray-600 text-sm ">Publisher : Level Invinite</p>

    <div class="flex flex-wrap">
      <span class="text-xs bg-gray-200 text-gray-700 px-2 py-1 rounded mr-2 mb-2">
        MMORPG
      </span>
      <p>{{ game }}</p>
    </div>
  </div>
</template>

<script setup>
</script>

<style></style>