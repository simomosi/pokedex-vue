<script setup>
const props = defineProps({
    pokemonCollection: Array,
    prevUrl: String|null,
    nextUrl: String|null
});

// Events and validators
const emit = defineEmits({
    prevClicked: (url) => {
        if (!url) {
            console.error("Invalid url in prev btn");
            return false;
        }
        return true;
    },
    nextClicked: (url) => {
        if (!url) {
            console.error("Invalid url in next btn", url);
            return false;
        }
        return true;
    },
    infoClicked: (url) => {
        if (!url) {
            console.error("Invalid url in info btn", url);
            return false;
        }
        return true;
    },
});

function emitInfoEvent(url) {
    emit('infoClicked', url);
}
function emitPrevEvent(url) {
    emit('prevClicked', url);
}
function emitNextEvent(url) {
    emit('nextClicked', url);
}
</script>

<template>
    <div class="container">
        <h2>Pokemon Journal</h2>
        <div v-if="pokemonCollection" class="row">
            <div v-for="p in pokemonCollection" class="col-4">
                {{ p.name }}
                <button type="button"@click="emitInfoEvent(p.url)" class="btn">
                    <i class="bi-search"></i>
                </button>
            </div> 
        </div>
        <p v-else>Loading...</p>

        <button type="button" v-if="prevUrl" @click="emitPrevEvent(prevUrl)" class="btn btn-primary">Previous</button>
        <button type="button" v-if="nextUrl" @click="emitNextEvent(nextUrl)" class="btn btn-primary">Next</button>
    </div>
</template>