<script setup>
import { RouterLink } from 'vue-router';
import {useGetData} from '@/composable/getData'

const {data,getData,loading,errorData}=useGetData()

getData('https://pokeapi.co/api/v2/pokemon');
</script>

<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando informacion</p>
  <div class="alert alert-danger" v-if="errorData">{{ errorData }}</div>
  <div v-else-if="data">
    <ul>
      <li v-for="pokemon in data.results" :key="pokemon.name">
        <RouterLink :to="`/pokemons/${pokemon.name}`">
          {{ pokemon.name }}
        </RouterLink>
      </li>
    </ul>
    <button class="button btn btn-warning" @click="getData(data.previous)">Previous</button>
    <button class="button btn btn-primary" @click="getData(data.next)">Next</button>
  </div>
</template>