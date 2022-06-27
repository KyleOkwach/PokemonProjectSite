<script>
export default {
  name: 'App',
  components: {
    Navbar,
    Searchbar,
    Footer,
    Pokedex
  }
}
</script>


<script setup>

import { ref, computed } from 'vue'
import Navbar from './components/Navbar.vue';
import Searchbar from './components/Searchbar.vue';
import Footer from './components/Footer.vue';
import Pokedex from './components/Pokedex.vue';
import { list } from 'postcss';

var query = 'pichu'
var limit = 36
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

const dex_sorted = ref(computed(() => {
  return dex.value.sort((a, b) => {
    return a.id - b.id
  })
}))

// console.log(dex)
// console.log(dex_sorted)
  
</script>

<template>
  <div class="flex flex-col h-screen">

    <Navbar />
  
    <Searchbar :inp="query"/>
  
  
    <!-- RESULTS -->
    <div class="flex justify-center ">
      <h2 class="text-green-500 uppercase text-xl">Pokedex</h2>
    </div>
  
    <Pokedex :api="dex_sorted"/>
  
    <Footer />

  </div>

</template>

<style>

</style>
