<script setup>

import { ref, computed } from 'vue'
import Navbar from './components/Navbar.vue';
import Searchbar from './components/Searchbar.vue';
import Footer from './components/Footer.vue';
import Pokedex from './components/Pokedex.vue';
import { list } from 'postcss';

var query = 'pichu'
var pokedexRange = {
  //Range of pokemon to display by ID
  rangeLower: 1,
  rangeUppper : 42
}
var search_result = {}
var dex = ref([])

var myDB = ref([])

const searchPokemon = () => {
  const url = `https://pokeapi.co/api/v2/pokemon/${ query }/`

  fetch(url)
    .then(res => res.json())
    .then(data => { search_result.value = data })

}

// GENERAL_LIST
const listPokemon = () => {

  for (let i = pokedexRange.rangeLower; i <= pokedexRange.rangeUppper; i++) {
    const url = `https://pokeapi.co/api/v2/pokemon/${ i }/`

    fetch(url)
      .then(res => res.json()) // 
      .then(data => { dex.value.push(data) })
    
  }

}


listPokemon()

const dex_sorted = ref(computed(() => {
  return dex.value.sort((a, b) => {
    return a.id - b.id
  })
}))
  
</script>

<template>
  <div class="flex flex-col h-screen">

    <Navbar />
  
    <!-- RESULTS -->
    <div class="flex justify-center ">
      <h2 class="text-blue-500 uppercase text-3xl">Pokedex</h2>
    </div>

    <Searchbar :inp="query"/>  
  
    <Pokedex :api="dex_sorted" :userDB="myDB" />
  
    <Footer />

  </div>

</template>

<style>

</style>
