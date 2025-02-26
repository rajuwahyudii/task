<template>
  <div class="min-h-screen bg-gray-900 text-white">
    <Navbar />
    <h1 class="text-3xl font-bold text-left m-8 text-white">Explorer Game</h1>
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
const config = useRuntimeConfig();
var games;
const { data, pending, error, refresh } = await useAsyncData(
  'pc-games',
  () => $fetch(`${config.public.apiBase}games?platform=pc`),
  {
    lazy: true,
    server: false,
  }
);

if (data.value && data.value.length > 0) {
  console.log(data.value[0].id);
}




</script>