<script>
    import Nav from "../components/nav.svelte";
</script>

<Nav></Nav>
<h1 class="mt-4 text-center text-3xl font-bold">Layout Page</h1>

<div class=" mt-10 w-[80%] mx-auto lg:flex ">
    <div class=" lg:w-[50%] h-[500px]  grid grid-cols-6 grid-rows-6 ">
        <div class="bg-sky-500 lg:col-span-2 lg:row-span-3 hidden lg:block"></div>
        <div class="bg-red-200 col-span-6 row-span-6 lg:col-span-4 lg:row-span-5"></div>
        <div class="bg-emerald-500 row-span-2 col-span-2 hidden lg:block"></div>
        <div class="bg-purple-500 row-span-1 col-span-6 hidden lg:block"></div>
    </div>
    
    <div class="lg:w-[50%] h-[500px] grid grid-cols-6 grid-rows-6">
        <div class="bg-cyan-400 col-span-6 row-span-2 hidden lg:block"></div>
        <div class="bg-yellow-200 col-span-6 row-span-6 lg:col-span-4 lg:row-span-4 flex items-center justify-center">
            <dir class="w-[50%] my-color h-[50%] flex justify-center items-center ">

                <div class="w-[130px] h-[120px] lg:h-[120px] mr-8 bg-yellow-200 rounded-full">

                </div>

            </dir>
        </div>
        <div class="bg-emerald-500 row-span-4 col-span-2 hidden lg:block"></div>
    </div>
</div>


<!-- Style -->

<style>

@tailwind base;
@tailwind components;
@tailwind utilities;

.b{
    border: 2px solid;
}

.my-color{
    background-color: #293462;
}
   
</style>