<template>
  <div>
    <div class="flex justify-center gap-2 p-6">
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

    <Meals :meals="meals" />
  </div>
</template>

<script setup>
import { computed, onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);

watch(route, () => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});

onMounted(() => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});
</script>