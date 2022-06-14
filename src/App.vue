<script>
export default {
  name: 'App',
  components: {
    Navbar,
    Searchbar,
    Footer
  }
}
</script>


<script setup>

import { ref, computed } from 'vue'
import Navbar from './components/Navbar.vue';
import Searchbar from './components/Searchbar.vue';
import Footer from './components/Footer.vue';
import { list } from 'postcss';

var query = 'pichu'
var limit = 151
var search_result = {}
var dex = ref([])

const searchPokemon = () => {
  const url = `https://pokeapi.co/api/v2/pokemon/${ query }/`

  fetch(url)
    .then(res => res.json())
    .then(data => { search_result.value = data })

}

// GENERAL_LIST
const listPokemon = () => {

  for (let i = 1; i <= limit; i++) {
    const url = `https://pokeapi.co/api/v2/pokemon/${ i }/`

    fetch(url)
      .then(res => res.json()) // 
      .then(data => { dex.value.push(data) })
    
  }

}

listPokemon()
console.log(dex)
  
</script>

<template>
  <div class="flex flex-col h-screen">

    <Navbar />
  
    <Searchbar :inp="query"/>
  
  
    <!-- RESULTS -->
    <div class="flex justify-center ">
      <h2 class="text-green-500 uppercase text-xl">Pokedex</h2>
    </div>
  
    <!-- CARD -->
    <div class="p-10 sm:grid sm:grid-cols-3 
      md:grid-cols-4 flex flex-col self-center
      items-center gap-10
    ">
  
      <div v-for="(pokemon, i) in dex" :key="i"
        class="text-white bg-slate-500 rounded-xl
        transition-all duration-300 overflow-hidden
        max-h-[200px] max-w-[164px] min-h-[200px] min-w-[164px]
        flex flex-col justify-between shadow-xl        
      ">
        <img :src="pokemon.sprites.other['official-artwork'].front_default" :alt="pokemon" />
        <ul class=" relative top-0 hover:top-[-60px]
          flex flex-col p-3 transition-all duration-500
          bg-gray-600 rounded-b-xl 
        ">
          <h3 class="uppercase">#{{ i+1 }} {{ pokemon.species.name }}</h3>
          <div class="flex gap-1">
            <p>Type: </p>
            <i v-for="(pkType, i) in pokemon.types" :key="i">{{ pkType.type.name }} </i>
          </div>
          <button 
            class="bg-green-700 hover:shadow-md mt-1
            hover:bg-green-500 hover:text-white rounded-md
            transition-all duration-300
          ">Add to DB</button>
        </ul>
      </div>
  
    </div>
  
    <Footer />

  </div>

</template>

<style>

</style>
