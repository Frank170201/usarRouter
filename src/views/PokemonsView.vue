<script setup>
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData.js";

const { data, getData, loading, errorData } = useGetData();

// const getData = async () => {
//   try {
//     const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon/");
//     pokemons.value = data.results;
//   } catch (error) {
//     console.log(error);
//   }
// };

getData("https://pokeapi.co/api/v2/pokemon/");
</script>


<template>
  <br />
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando informacion</p>
  <div class="alert alert-danger" v-if="errorData">{{ errorData }}</div>
  <br />
  <div v-if="data">
    <ul class="list-group">
      <li
        v-for="(poke, index) in data.results"
        :key="index"
        class="list-group-item"
      >
        <router-link :to="`/pokemons/${poke.name}`">{{
          poke.name
        }}</router-link>
      </li>
    </ul>
    <div class="mt-2">
      <button
        :disabled="!data.previous"
        class="btn btn-success me-2"
        @click="getData(data.previous)"
      >
        Previous
      </button>
      <button
        :disabled="!data.next"
        class="btn btn-primary"
        @click="getData(data.next)"
      >
        Next
      </button>
    </div>
  </div>
</template>