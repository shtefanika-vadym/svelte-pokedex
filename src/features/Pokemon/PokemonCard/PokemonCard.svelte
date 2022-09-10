<script>
  import { createEventDispatcher, onMount } from 'svelte'

  const dispatch = createEventDispatcher()

  export let pokemonData
  export let pokemonClick = () => {}

  let pokemonDetails

  onMount(async () => {
    const response = await fetch(pokemonData?.url)
    const pokemonInfo = await response.json()
    pokemonDetails = pokemonInfo
  })

  function handleClickOnPokemon() {
    dispatch('pokemonClick', pokemonDetails)
  }
</script>

<div on:click={handleClickOnPokemon} class="card">
  <div
    class="card-header"
    style="background-image: url({pokemonDetails?.sprites?.other?.dream_world?.front_default})" />

  <div class="card-body">
    <h2 class="name">{pokemonDetails?.name}</h2>
    <h4 class="total-exp">{pokemonDetails?.base_experience} XP</h4>
    <div class="bio">
      {#if pokemonDetails?.abilities.length > 0}
        {#each pokemonDetails?.abilities as ability}
          <span class='ability'>{ability?.ability?.name}</span>
        {/each}
      {/if}
    </div>
  </div>

  <div class="card-footer">
    <div class="stats">
      <div class="stat">
        <span class="label">Weight</span>
        <span class="value">{pokemonDetails?.weight} kg</span>
      </div>
      <div class="stat">
        <span class="label">Height</span>
        <span class="value">{pokemonDetails?.height} m</span>
      </div>
    </div>
  </div>
</div>

<style>
  .card {
    position: relative;
    width: 315px;
    height: 450px;
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid var(--color-light);
  }
  .card:hover {
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  }
  .card-header {
    position: relative;
    height: 240px;
    background-size: cover;
    background-position: top;
  }
  .card-header:after {
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    background: linear-gradient(to top, rgb(5, 85, 134), rgba(181, 181, 181, 0.1));
  }

  .card-body {
    text-align: center;
    padding: 10px;
  }

  .name {
    font-size: 20px;
    font-weight: 700;
    text-transform: uppercase;
    margin: 0 auto;
  }

  .total-exp {
    font-size: 14px;
    font-weight: 300;
    margin-top: 5px;
    color: #919191;
  }

  .bio {
    display: flex;
  }

  .ability {
    font-size: 14px;
    color: #7b7b7b;
    font-weight: 300;
    margin: 10px auto;
    line-height: 20px;
  }

  .card-footer {
    position: absolute;
    left: 0;
    width: 100%;
    bottom: 20px;
  }
  .stat {
    box-sizing: border-box;
    width: calc(100% / 2);
    float: left;
    text-align: center;
  }

  .stat:first-child {
    border-right: 1px solid #ebebeb;
  }

  .stat .label {
    display: block;
    text-transform: uppercase;
    font-weight: 300;
    font-size: 11px;
    letter-spacing: 1px;
    color: #95989a;
  }

  .stat .value {
    display: block;
    font-weight: 700;
    font-size: 20px;
    margin-top: 5px;
  }
</style>
