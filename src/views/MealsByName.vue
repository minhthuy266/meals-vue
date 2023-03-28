<template>
  <div>
    <input
      type="text"
      v-model="keyword"
      class="rounded border-gray-200 w-full mx-4 my-4"
      placeholder="Search for meals"
      @change="searchMeals"
    />
  </div>

  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";
import store from "../store";
import Meals from "../components/Meals.vue";
import { useRoute } from "vue-router";

const route = useRoute();

const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
  keyword.value = route.params.name;

  if (keyword.value) {
    searchMeals();
  }
});
</script>