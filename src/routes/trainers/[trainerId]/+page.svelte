<script>
  import { page } from "$app/state";
  import { onMount } from "svelte";
  import LoadingSpinner from "$lib/components/LoadingSpinner.svelte";
  import TrainerHeader from "$lib/components/TrainerHeader.svelte";
  import PokemonCard from "$lib/components/PokemonCard.svelte";
  import { PUBLIC_BASE_URL } from "$env/static/public";

  let trainer = $state(null);
  let loading = $state(true);
  let error = $state(null);

  let trainerId = $derived(page.params.trainerId);
  $effect(() => loadTrainer(trainerId));

  async function loadTrainer(trainerId) {
    try {
      loading = true;
      const response = await fetch(`${PUBLIC_BASE_URL}/api/trainers/${trainerId}`);
      if (!response.ok) {
        throw new Error("Trainer not found");
      }
      trainer = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  }
</script>

<svelte:head>
  <title>{trainer ? `${trainer.name} - Trainer Details` : "Loading Trainer..."}</title>
</svelte:head>

<div class="trainer-detail-container">
  {#if loading}
    <LoadingSpinner text="Loading trainer details..." />
  {:else if error}
    <div class="error-message">
      <h1>❌ Error</h1>
      <p>{error}</p>
      <a href="/trainers" class="back-link">← Back to Trainers</a>
    </div>
  {:else if trainer}
    <TrainerHeader {trainer} />

    <div class="pokemon-team-section">
      <h2>Pokémon Team</h2>
      {#if trainer.team && trainer.team.length > 0}
        <div class="pokemon-grid">
          {#each trainer.team as pokemon}
            <PokemonCard {pokemon} />
          {/each}
        </div>
      {:else}
        <p class="no-pokemon">This trainer doesn't have any Pokémon in their team.</p>
      {/if}
    </div>
  {/if}
</div>

<style>
  .trainer-detail-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .error-message {
    text-align: center;
    padding: 4rem 2rem;
  }

  .error-message h1 {
    color: #d32f2f;
    margin-bottom: 1rem;
  }

  .error-message p {
    color: #666;
    font-size: 1.1rem;
    margin-bottom: 2rem;
  }

  .pokemon-team-section {
    background: white;
    border-radius: 16px;
    padding: 2rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .pokemon-team-section h2 {
    color: #2e7d32;
    font-size: 2rem;
    font-weight: 600;
    margin: 0 0 2rem 0;
    text-align: center;
  }

  .pokemon-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .no-pokemon {
    text-align: center;
    color: #666;
    font-style: italic;
    font-size: 1.1rem;
    padding: 2rem;
  }

  @media (max-width: 768px) {
    .trainer-detail-container {
      padding: 1rem 0.5rem;
    }

    .pokemon-grid {
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
    }

    .pokemon-team-section {
      padding: 1.5rem;
    }
  }

  @media (max-width: 480px) {
    .pokemon-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
