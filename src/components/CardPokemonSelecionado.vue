<script setup>
const pokemon = defineProps(["name", "xp", "height", "img", "loading"]);

</script>

<template>
<div class="card card-pokemon-selecionado cardPokemonSelecionado"
:class="loading ? '' : 'animate__animated animate__flipInY'">
    <img
    v-if="pokemon.name" 
    :src="pokemon.img"
    class="card-img-top custom-padding" 
    height="420"
    :alt="pokemon.name"
    >
    <img 
    v-else
    src="../assets/ovo.png" 
    class="card-img-top custom-padding" 
    height="420" 
    alt=""
    >

    <div class="card-body">
        <h3 class="card-title text-center text-uppercase pt-5 fs-1">{{ pokemon?.name|| '???' }}</h3>
        <hr>
        <br>
        <div class="row pt-1">
            <section class="text-center fs-2">
                <strong>XP: </strong>
                <span>{{ pokemon.xp }}</span>
            </section>
            <section class="text-center fs-2">
                <strong text-h-5>Altura: </strong>
                <span>{{ pokemon.height }}</span>
            </section>
        </div>
    </div>
</div>
</template>