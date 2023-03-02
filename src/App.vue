<script setup>
import Home from "./views/Home.vue";
</script>

<template>
  <div class="bg-gray-100 h-full">
    <header class="bg-white shadow-md h-16 flex justify-between items-center">
      <router-link :to="{ name: 'home' }"> Home </router-link>

      <div>
        <router-link
          :to="{ name: 'home' }"
          class="px-2 h-full hover:bg-purple-200"
        >
          Search Neals
        </router-link>

        <router-link
          :to="{ name: 'home' }"
          class="px-2 h-full hover:bg-purple-200"
        >
          Meals By Letter
        </router-link>

        <router-link
          :to="{ name: 'home' }"
          class="px-2 h-full hover:bg-purple-200"
        >
          Meals By Ingredients</router-link
        >
      </div>
    </header>

    <main>
      <router-view />
    </main>
  </div>
</template>

<style scoped>
</style>
