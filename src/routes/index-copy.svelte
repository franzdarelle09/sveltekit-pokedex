<script>
    import {pokemon} from "../stores/pokestore"
    import Pokecard from '../components/pokecard.svelte'


    let searchTerm = "";
    let filteredPokemon = [];

    $: {
        if(searchTerm){
            filteredPokemon = $pokemon.filter(poke => poke.name.toLowerCase().includes(searchTerm.toLowerCase()))
        }else{
            filteredPokemon = [...$pokemon]
        }
    }
</script>
<svelte:head>
    <title>Home | Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>
<input bind:value={searchTerm} type="text" placeholder="Search Pokemon" class="w-full rounded-md text-lg p-4 border-2 border-gray-200" />
<div class="py-4 grid gap-4 md:grid-cols-3 grid-cols-1">
{#each filteredPokemon as poke}
    <Pokecard poke={poke} />
{/each}
</div>