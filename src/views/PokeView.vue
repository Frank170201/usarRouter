<script setup>
import { useRoute, useRouter } from "vue-router";
import {useGetData} from '@/composables/getData.js'


const route = useRoute();
const router = useRouter();
const {getData,data,loading,errorData}=useGetData()


// const poke = ref({});

const back = () => {
  router.push("/pokemons");
};

// const getData = async () => {
//   try {
//     const { data } = await axios.get(
//       `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
//     );
//     poke.value = data;
//   } catch (error) {
//     console.log(error);
//     poke.value = null;
//   }
// };

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <p v-if="loading">Cargando informacion</p>
  <div class="alert alert-danger" v-if="errorData"> {{ errorData }}</div>
  <div v-if="data">
    <img :src="data.sprites?.front_default" alt="" />
    <h1>Pokemon name: {{ $route.params.name }}</h1>
  </div>
  <button @click="back()" class="btn btn-outline-primary">Volver</button>
</template>