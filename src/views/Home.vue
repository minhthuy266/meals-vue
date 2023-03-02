<template>
  <div class="flex p-8 items-center justify-center">
    <div>
      <input
        type="text"
        class="rounded border-gray-200 w-full"
        placeholder="Search for meals"
      />

      <div class="flex gap-2 mt-2">
        <router-link
          v-for="(letter, index) of letters"
          :key="index"
          :to="{ name: 'byLetter', params: { letter } }"
        >
          <span class="mr-1 ml-1">
            {{ letter }}
          </span>
        </router-link>
      </div>

      <pre>
        <!-- {{ ingredients }} -->
      </pre>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient";

const meals = computed(() => store.state.meals);

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");

const ingredients = ref([]);

onMounted(async () => {
  const response = await axiosClient.get("/list.php?i=list");

  ingredients.value = response.data;
});
</script>