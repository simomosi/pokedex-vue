<script setup>
const props = defineProps({
    pokemon: Object
})
</script>

<template>
    <div class="container">
        <h2>Profile</h2>
        <div class="row">
            <div class="col-1">
                <img :src="pokemon.frontSprite" width="75" height="75"/>
                <img :src="pokemon.backSprite" width="75" height="75"/>
            </div>
            <div class="col">
                <ul>
                    <li>Name: {{ pokemon.name }}</li>
                    <li>Types: {{ pokemon.types.join(', ') }}</li>
                    <li>Height: {{ pokemon.height }}</li>
                    <li>Weight: {{ pokemon.weight }}</li>
                </ul>
                <audio controls>
                    <source :src="pokemon.cry" type="audio/ogg">
                    Your browser does not support the audio element.
                </audio> 
            </div>
        </div>
    </div>
</template>