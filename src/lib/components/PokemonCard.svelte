<script>
  import TypeBadge from "./TypeBadge.svelte";

  let { pokemon } = $props();
</script>

<div class="pokemon-card">
  <div class="pokemon-image">
    <img src={pokemon.image} alt={pokemon.name} loading="lazy" />
    {#if pokemon.isShiny}
      <span class="shiny-badge">✨</span>
    {/if}
  </div>
  <div class="pokemon-info">
    <h3 class="pokemon-name">{pokemon.nickname || pokemon.name}</h3>
    {#if pokemon.nickname && pokemon.nickname !== pokemon.name}
      <p class="pokemon-species">({pokemon.name})</p>
    {/if}
    <p class="pokemon-level">Level {pokemon.level}</p>
    <div class="pokemon-types">
      {#each pokemon.types as type (type.toLowerCase())}
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
    transition:
      transform 0.2s ease,
      box-shadow 0.2s ease;
    border: 2px solid transparent;
  }

  .pokemon-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
    border-color: #e8f5e8;
  }

  .pokemon-image {
    text-align: center;
    margin-bottom: 1rem;
    position: relative;
  }

  .pokemon-image img {
    width: 120px;
    height: 120px;
    object-fit: contain;
  }

  .shiny-badge {
    position: absolute;
    top: -5px;
    right: 10px;
    color: #333;
    font-size: 2.5rem;
    text-shadow:
      0 0 5px #ffd700,
      0 0 10px #ffd700,
      0 0 15px #ffd700,
      0 0 20px #ffd700;
  }

  .pokemon-info {
    text-align: center;
  }

  .pokemon-name {
    color: #2e7d32;
    font-size: 1.3rem;
    font-weight: 600;
    margin: 0 0 0.25rem 0;
  }

  .pokemon-species {
    color: #666;
    font-size: 0.9rem;
    font-style: italic;
    margin: 0 0 0.5rem 0;
  }

  .pokemon-level {
    color: #4caf50;
    font-weight: 600;
    margin: 0 0 1rem 0;
    font-size: 1.1rem;
  }

  .pokemon-types {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  @media (max-width: 768px) {
    .pokemon-card {
      padding: 1rem;
    }
  }
</style>
