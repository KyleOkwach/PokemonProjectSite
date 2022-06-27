<script>
export default{
    name: 'Pokedex',
    props: {
        api: { type: Array }
    }
}
</script>

<template>
    <div class="p-10 sm:grid sm:grid-cols-3 
      md:grid-cols-4 xl:grid-cols-5
      flex flex-col self-center
      items-center gap-10
    ">
  
      <div v-for="(pokemon, i) in api" :key="i"
        class="text-white bg-gradient-to-tr from-gray-900/50 via-slate-700/60 to-gray-900/50
        rounded-xl bg-opacity-10 shadow-xl
        transition-all duration-300 overflow-hidden
        max-h-[200px] max-w-[164px] min-h-[200px] min-w-[164px]
        flex flex-col justify-between      
      ">
        <img :src="pokemon.sprites.other['official-artwork'].front_default" :alt="pokemon.species.name + ' sprite'" />
        <ul class=" relative top-0 hover:top-[-60px]
          flex flex-col p-2 transition-all duration-500
          bg-gradient-to-t from-gray-900 to-transparent
          items-center
        ">
          <h3 class="uppercase mb-1">#{{ pokemon.id }} {{ pokemon.species.name }}</h3>
          <div class="flex gap-1">
            <p>Type: </p>
            <div class="flex">
              <i class="flex" v-for="(pkType, i) in pokemon.types" :key="i"><i v-if="i > 0">/</i>{{ pkType.type.name }}</i>
            </div>
          </div>
          <button 
            class="bg-green-700 hover:shadow-md mt-1
            hover:bg-green-500 hover:text-white rounded-md
            transition-all duration-300 px-2 hover:px-3
          ">Add to DB</button>
        </ul>
      </div>
  
    </div>
</template>
