<template>
  <div class="bg-white rounded-lg shadow-md p-4 cursor-pointer transform transition hover:scale-105">
    <div class="w-full flex mb-4">
      <img class="mx-auto" :src="data.thumbnail" alt="thumbnail">
    </div>
    <h3 class="font-semibold text-black text-lg mb-2">{{ data.title }}</h3>
    <p class="text-gray-600 text-sm mb-4 line-clamp-3">{{ data.short_description }}</p>

    <div class="flex flex-wrap">
      <span class="text-xs bg-gray-200 text-gray-700 px-2 py-1 rounded mr-2 mb-2">
        {{ data.genre }}
      </span>
    </div>
    <p class="text-gray-600 text-sm ">Publisher : {{ data.publisher }}</p>
    <p class="text-gray-600 text-sm ">Platform : {{ data.platform }}</p>
  </div>

</template>

<script setup>
const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
});
const { data } = props;
</script>

<style></style>