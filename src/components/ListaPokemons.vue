<script setup>
const pokemon = defineProps(["name","urlImagem"])

</script>

<template>
    <div class="col-4">
        <div class="card m-2 cardList card-pokemon">
            <img :src="urlImagem" class="card-img-top mt-3" alt="..." height="120">
            <p class="text-center text-uppercase m-2">{{ pokemon.name }}</p>
        </div>
    </div>
</template>

<style scoped>
</style>