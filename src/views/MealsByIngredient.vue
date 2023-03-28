<template>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";
import store from "../store";

const route = useRoute();

const meals = computed(() => store.state.mealsByIngredients);

onMounted(() => {
  store.dispatch("searchMealsByIngredient", route.params.ingredient);
});
</script>