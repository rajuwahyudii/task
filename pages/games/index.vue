<template>
  <div class="min-h-screen bg-gray-900 text-white">
    <Navbar />
    <h1 class="text-3xl font-bold text-left m-8 text-white">Explorer Game</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 p-2">
      <!-- loading -->
      <div class="flex justify-center items-center py-12">
        <Loading></Loading>
      </div>
      <!-- error -->
      <Error></Error>
      <Card>
      </Card>
    </div>
  </div>
</template>

<script setup>
const { data, pending, error, refresh } = await useFetch('https://www.mmobomb.com/api1/games?platform=pc', {
  lazy: true,
  server: false,
})
console.log(data.value)



</script>