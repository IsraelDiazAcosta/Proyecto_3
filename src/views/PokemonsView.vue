<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';

const pokemons = ref([]);

const getData = async () => {
  try {
    const { data } = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=20');
    pokemons.value = data.results ?? [];
  } catch (error) {
    console.error('Error al cargar pokémones:', error);
  }
};

onMounted(() => {
  getData();
});
</script>

<template>
  <h1>Pokemons</h1>

  <ul v-if="pokemons.length">
    <li v-for="pokemon in pokemons" :key="pokemon.name">
      <RouterLink :to="`/pokemons/${pokemon.name}`">
        {{ pokemon.name }}
      </RouterLink>
    </li>
  </ul>

  <p v-else>Cargando pokémones...</p>
</template>