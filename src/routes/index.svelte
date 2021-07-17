<script context="module">
    export async function load({page}){
        const url = `https://pokeapi.co/api/v2/pokemon?limit=898`;
        const res = await fetch(url);
        const data = await res.json();
        const loadedPokemon = data.results.map((data,index) => {
            return {
                id: index + 1,
                name: data.name,
                image: `https://raw.githubusercontent.com/POKEAPI/sprites/master/sprites/pokemon/${index+1}.png`,
                url: data.url
            }
        })
        return {props: {pokemon: loadedPokemon}}
    }
</script>
<script>
    export let pokemon
    import Pokecard from '../components/pokecard.svelte'

    let searchTerm = "";
    let filteredPokemon = [];

    $: {
        if(searchTerm){
            filteredPokemon = pokemon.filter(poke => poke.name.toLowerCase().includes(searchTerm.toLowerCase()))
        }else{
            filteredPokemon = [...pokemon]
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