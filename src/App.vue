<script setup>
import { ref } from 'vue';
import FiltroRegion from './components/FiltroRegion.vue';
import PokemonCard from './components/PokemonCard.vue';

const error = ref('');
const pokemons = ref([]);
// Ir a la pokeAPI y cargar los Pokémon de la región seleccionada
async function cargarPorRegion(regionId){
    error.value = '';
    pokemons.value =[];

    try{
      const res = await fetch(`https://pokeapi.co/api/v2/pokedex/${regionId}`);
      const data = await res.json();

      //seleccionar los primeros 50 Pokémon de la región
      const pokemonlist = data.pokemon_entries.slice(0, 50);

      //cargar los datos de cada Pokémon
      const detalles = await Promise.all(
        pokemonlist.map(entry => fetch(entry.pokemon_species.url.replace('pokemon-species', 'pokemon')).then(res => res.json()))
      )
      console.log(detalles);


      console.log(data);
    } catch (e) {
      error.value = 'Error al cargar los Pokémon de la región seleccionada';
      console.error(e, error.value);
      alert(error.value);

    }

}
</script>

<template>
<h1>Selector de Pokémon por región</h1>
<FiltroRegion @cambio-region="cargarPorRegion" />
<div v-if="pokemons.length" class="grid">
  <PokemonCard/>
</div>
<div v-else>
  <p>No hay pokemons para mostrar</p>
</div>
</template>

<style scoped>
.grid{
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}
</style>
