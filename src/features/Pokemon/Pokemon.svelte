<script>
  import { onMount } from 'svelte'
  import PokemonCard from './PokemonCard/PokemonCard.svelte'

  let pokemonData = []
  let filterValue = ''
  let filteredPokemonData = []

  $: filteredPokemonData = filterPokemonData(pokemonData, filterValue)

  function filterPokemonData(pokemons, name) {
    return pokemons.filter((pokemon) => pokemon.name.toLowerCase().includes(name.toLowerCase()))
  }

  function handleClickOnPokemon(event) {
    console.log(event.detail)
  }

  onMount(async () => {
    const response = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=10`)
    const pokemons = await response.json()
    pokemonData = pokemons.results
  })
</script>

<div>
  <div class="pokemon-filter">
    <label class="filter-label" for="filterInput">Filter by name</label>
    <input
      class="filter-input"
      id="filterInput"
      bind:value={filterValue}
      type="text"
      placeholder="Type here" />
  </div>

  <div class="pokemon-list">
    {#if filteredPokemonData.length > 0}
      {#each filteredPokemonData as pokemon}
        <PokemonCard on:pokemonClick={handleClickOnPokemon} pokemonData={pokemon} />
      {/each}
    {:else}
      <h3>No pokemon was found by name {filterValue}</h3>
    {/if}
  </div>
</div>

<style>
  .pokemon-list {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  .pokemon-filter {
    display: flex;
    flex-direction: column;
    width: 30%;
    margin: 0 auto;
    padding: 20px 0 100px 0;
  }

  .filter-label {
    font-style: normal;
    font-weight: 500;
    font-size: 13px;
    line-height: 20px;
    color: var(--color-dark);
  }

  .filter-input {
    padding: 11px 12px 11px 12px;
    border: 1px solid #d1d1d6;
    border-radius: 6px;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 18px;
  }

  .filter-input:focus {
    outline: none;
  }
</style>
