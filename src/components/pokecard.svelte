<script>
    import {fade} from 'svelte/transition'
    export let poke
</script>
<a href={`/pokemon/${poke.id}`} class="p-6 bg-gray-100 text-gray-800 text-center rounded-md shadow-sm hover:shadow-md flex flex-col items-center" transition:fade>
    <img src={poke.image} alt={poke.name} class="h-40 w-40">
    <h2 class="uppercase text-2xl">{poke.id}. {poke.name}</h2>
</a>
<style></style>