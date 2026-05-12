<script>
  import TypeBadge from "./TypeBadge.svelte";
  let { pokemon } = $props();
</script>

<div class="pokemon-card">
  <div class="pokemon-image">
    <img src={pokemon.image} alt={pokemon.name} />
    {#if pokemon.isShiny}
      <span class="shiny-badge">✨</span>
    {/if}
  </div>
  <div class="pokemon-info">
    <h3 class="pokemon-name">{pokemon.nickname || pokemon.name}</h3>
    <p class="pokemon-level">Level {pokemon.level}</p>
    <div class="pokemon-types">
      {#each pokemon.types as type}
        <TypeBadge {type} />
      {/each}
    </div>
  </div>
</div>

<style>
  .pokemon-card {
    background: #f8f9fa;
    border-radius: 12px;
    padding: 1.5rem;
    transition: transform 0.2s ease;
  }
</style>