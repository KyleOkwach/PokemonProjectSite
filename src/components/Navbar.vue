<script>
export default{
    setup() {
        name: "Navbar"
    },
}
</script>

<template>
    <nav class="text-white flex bg-gray-700 fixed
    justify-center z-20
    sm:justify-between px-3 items-center h-10 shadow-md
    w-[100%]">
        <h1 class="text-2xl">PokeDB</h1>
        <ul class="hidden sm:flex sm:gap-5">
            <li class="nav-link"><a href="">Search</a></li>
            <li class="nav-link"><a href="">Pokedex</a></li>
            <li class="nav-link"><a href="">MyDB</a></li>
        </ul>
    </nav>
    <br>
    <br>
</template>
