<script setup>

import axios from 'axios';
import { ref, onMounted } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
const pokemons = ref([]);

const getData= async() =>{
    try{
        const {data}= await axios.get('https://pokeapi.co/api/v2/pokemon')
        console.log(data.results)
        pokemons.value=data.results
    }catch(error){
        console.log(error)
    }
     
}
getData();
</script>

<template>
<h1>Pokemons</h1>

<ul>
    <li v-for="pokemon in pokemons" :key="pokemon.name">
        <RouterLink :to="`/pokemons/${poke.name}`">
            {{pokemon.name}}
        </RouterLink>
        
    </li>
</ul>

</template>