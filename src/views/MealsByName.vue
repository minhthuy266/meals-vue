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

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div
      v-for="meal of meals"
      :key="meal?.idMeal"
      class="bg-white shadow rounded-xl pb-3"
    >
      <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
        <img
          :src="meal?.strMealThumb"
          :alt="meal?.strMeal"
          class="rounded-t-xl w-full h-64 object-cover"
        />
      </router-link>

      <div class="p-3">
        <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
          <h3 class="font-bold">
            {{ meal?.strMeal }}
          </h3>

          <p class="mb-4">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Repellat
            cum praesentium eos sit expedita modi minima magni facere placeat
            vitae!
          </p>
        </router-link>

        <div>
          <a
            :href="meal?.strYoutube"
            target="_blank"
            class="px-3 py-2 rounded border-2 text-white border-red-600 bg-red-500 hover:bg-red-600 transition:colors"
          >
            Youtube
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";
import store from "../store";
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