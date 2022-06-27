<script>
export default{
    name: 'Pokedex',
    props: {
        api: { type: Array },
        userDB: { type: Array, required: false },
        rangeFrom: Number,
        rangeTo: Number
    },
    methods: {
      addToDB(pkmn){
        this.userDB.push(pkmn)
        console.log(this.userDB)
      },
      removeFromDB(pkmn){
        this.userDB.splice(this.userDB.indexOf(pkmn))
        console.log(this.userDB)
      },
      openPage(pkmn){
        console.log(pkmn)
      }
    }
}
</script>

<template>
    <div
      class="
        flex justify-center mt-6 gap-2
      "
    >
      <h3 class="text-white text-xl uppercase">Range</h3>
      <form class="flex gap-2">
        <input type="number" placeholder="From" class="range-field"/>
        <input type="number" placeholder="To" class="range-field"/>
      </form>
    </div>

    <div class="p-10 sm:grid sm:grid-cols-3 
      md:grid-cols-4 xl:grid-cols-5
      flex flex-col self-center
      items-center gap-10
    ">
  
      <div v-for="(pokemon, i) in api" :key="i"
        class="text-white bg-gradient-to-tr from-gray-900/50 via-blue-900/60 to-gray-900/50
        rounded-xl bg-opacity-10 shadow-xl
        transition-all duration-300 overflow-hidden
        max-h-[200px] max-w-[164px] min-h-[200px] min-w-[164px]
        flex flex-col justify-between      
      ">
        <div class="h-[100%]">
          <img :src="pokemon.sprites.other['official-artwork'].front_default" :alt="pokemon.species.name + ' sprite'" />
        </div>
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
          <div class="flex gap-2">
            <button 
              @click="openPage(pokemon)"
              class="bg-green-700 hover:bg-green-500 dex-button">
                <i>Data</i>
            </button>

            <button 
              v-if="!userDB.includes(pokemon)"
              @click="addToDB(pokemon)"
              class="dex-button hover:bg-green-500 bg-green-700">
                <i class="fa-solid fa-database"></i>
                <i>+</i>
            </button>

            <button 
              v-if="userDB.includes(pokemon)"
              @click="removeFromDB(pokemon)"
              class="dex-button hover:bg-red-600 bg-red-500">
                <i class="fa-solid fa-database"></i>
                <i>-</i>
            </button>
          </div>
        </ul>
      </div>
  
    </div>
</template>
