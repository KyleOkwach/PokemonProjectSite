<script>
import { ref, computed } from 'vue'

export default{
    name: "Searchbar",
    props: {
        inp: ''
    }
}
</script>

<template>
    <div class="search flex gap-2 justify-center">
        <form @submit.prevent="searchPokemon"
            class="shadow-xl"
        >
            <input type="text" v-model="inp.value" 
                class="rounded-l-xl">
            <button class="bg-gray-600 hover:bg-gray-500 
                rounded-r-xl px-1 transition-all 
                duration-300 text-white
            "
            >
                <i class="fa-solid fa-magnifying-glass"></i>
            </button>
        </form>

    </div>
</template>