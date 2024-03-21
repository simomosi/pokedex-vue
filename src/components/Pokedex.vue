<script setup>
import {ref} from 'vue'
import Journal from './Journal.vue';
import PokemonCard from './PokemonCard.vue';

const defaultPokemonUrl = "https://pokeapi.co/api/v2/pokemon/";
const collection = ref([]);
const prevUrl = ref(null);
const nextUrl = ref(null)

const selectedPokemon = ref(null);

async function fetchPokemonList(url) {
    const result = await fetch(url).then(r => r.json());
    collection.value = result.results;
    prevUrl.value = result.previous;
    nextUrl.value = result.next;
}

async function fetchSinglePokemon(url) {
    const result = await fetch(url).then(r => r.json());
    console.log(result);
    selectedPokemon.value = {
        id: result.id,
        name: result.name,
        frontSprite: result.sprites.front_default,
        backSprite: result.sprites.back_default,
        types: result.types.map(e => e.type.name),
        height: result.height,
        weight: result.weight,
        cry: result.cries.legacy
    }
}
fetchPokemonList(defaultPokemonUrl);

</script>

<template>
    <Journal 
    :pokemonCollection="collection" 
    :prevUrl="prevUrl" 
    :nextUrl="nextUrl" 
    @prevClicked="fetchPokemonList" 
    @nextClicked="fetchPokemonList"
    @infoClicked="fetchSinglePokemon"
    />

    <div class="mt-3"></div>
    <PokemonCard v-if="selectedPokemon" :pokemon="selectedPokemon"/>
</template>