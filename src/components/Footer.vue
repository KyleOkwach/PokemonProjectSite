<script>
export default{
    name: "Footer"
}
</script>

<template>
    <footer class="bg-gray-700 h-10 w-[100%] bottom-0 
        flex flex-col justify-center items-center mt-[100px]
        text-gray-300 p-[60px]
    ">
        <div>KyleOkwach | 2022</div>
        <div class="flex gap-2 divide-x">
            <div class="foot-tab">
                <h2 class="underline">Contact Me</h2>
                <ul>
                    <li>example@gmail.com</li>
                    <li>+254123123456</li>
                </ul>
            </div>
            <div class="foot-tab">
                <h2 class="underline">Socials</h2>
                <ul class="flex gap-2">
                    <li class="foot-link"><a href="">A</a></li>
                    <li class="foot-link"><a href="">B</a></li>
                    <li class="foot-link"><a href="">C</a></li>
                </ul>
            </div>
        </div>
    </footer>
</template>