<template>
  <div class="flex p-8 items-center justify-center">
    <div>
      <input
        type="text"
        class="rounded border-gray-200 w-full"
        placeholder="Search for meals"
      />

      <MealByLetter />

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
import MealsByLetter from "./MealsByLetter.vue";

const meals = computed(() => store.state.meals);

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");

const ingredients = ref([]);

onMounted(async () => {
  const response = await axiosClient.get("/list.php?i=list");

  ingredients.value = response.data;
});
</script>