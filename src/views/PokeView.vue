<script setup>

import {useRoute, useRouter} from 'vue-router'
import {useGetData} from '@/composable/getData'


const route =useRoute();
const router =useRouter();

const {data,getData,loading,errorData}=useGetData()


const back=()=>{

    router.push('/pokemons')
}

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
</script>


<template>
    <p v-if="loading">Cargando informacion</p>
    <div class="alert alert-danger" v-if="errorData">{{ errorData }}</div>


        <div v-if="data">
            <img :src="data.sprites?.front_default" alt="">
            <h1>Poke name: {{ $route.params.name}}</h1>
        </div>
        <h1 v-else>
            No existe ese pokemon
        </h1>
    <button @click="back" class="btn btn-outline-primary">Volver</button>

</template>