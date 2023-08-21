<script setup>
import { onMounted, reactive, ref, computed } from "vue";
import ListaPokemons from "../components/ListaPokemons.vue"
import CardPokemonSelecionado from "../components/CardPokemonSelecionado.vue"

let pokemons = reactive(ref())
let urlImagemPokemon = 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/';
let buscaPokemon = ref('');
let pokemonSelecionado = reactive(ref());
let loading = ref(false);


onMounted(async () => {
  await fetch(`https://pokeapi.co/api/v2/pokemon?limit=151&offset=0`)
  .then(res => res.json())
  .then(res => pokemons.value = res.results);
});

const pokemonFiltragem = computed(() => {
  if(pokemons.value && buscaPokemon.value){
    return pokemons.value.filter(pokemon => 
      pokemon.name.toLowerCase().includes(buscaPokemon.value.toLowerCase())
    )
  }
  return pokemons.value
});

const selecionarPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelecionado.value = res)
  .catch(err => alert(err))
  .finally(() => {
    loading.value = false;
  });
}

</script>

<template>
  <main>
    <div class="container">

      <div class="row mt-5">
        <div class="col-sm-12 col-md-6">
          <div class="card card-list card-listagem">
            <div class="input-group mb-3">
                <label 
                    hidden 
                    for="campoBuscarPokemon" 
                    class="form-label"
                >Buscar Pokemon</label>
                <input v-model="buscaPokemon"
                    type="text" 
                    class="form-control" 
                    id="campoBuscarPokemon" 
                    placeholder="Buscar...">
            </div>

            <div class="card-body row scroll-container">
                <ListaPokemons
                    v-for="pokemon in pokemonFiltragem"
                    :key="pokemon.name"
                    :name="pokemon.name"
                    :urlImagem="urlImagemPokemon + pokemon.url.split('/')[6] + '.svg'"
                    @click="selecionarPokemon(pokemon)"/>
            </div>
          </div>
        </div>

        <div class="col-sm-12 col-md-6">
          <CardPokemonSelecionado 
         :name="pokemonSelecionado?.name"
         :xp="pokemonSelecionado?.base_experience"
         :height="pokemonSelecionado?.height"
         :img="pokemonSelecionado?.sprites.other.dream_world.front_default"
         :loading="loading"/>
        </div>
      </div>

    </div>
  </main>
</template>

<style scoped>

</style>
