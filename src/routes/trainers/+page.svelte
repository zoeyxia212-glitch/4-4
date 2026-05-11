<script>
  import { PUBLIC_BASE_URL } from "$env/static/public";
  import { onMount } from "svelte";
  import LoadingSpinner from "$lib/components/LoadingSpinner.svelte";
  import TrainerCard from "$lib/components/TrainerCard.svelte";

  let trainers = $state([]);

  // Fetch the list of trainers from the API when the component is mounted
  onMount(async () => {
    const res = await fetch(`${PUBLIC_BASE_URL}/api/trainers`);
    const data = await res.json();
    trainers = data;
  });
</script>

<svelte:head>
  <title>Trainer database</title>
</svelte:head>

<div class="trainers-container">
  <h1>Pokémon Trainer Database</h1>

  {#if trainers.length === 0}
    <LoadingSpinner text="Loading trainers..." />
  {:else}
    <div class="trainers-grid">
      {#each trainers as trainer (trainer.trainerId)}
        <TrainerCard {trainer} />
      {/each}
    </div>
  {/if}
</div>

<style>
  .trainers-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  h1 {
    text-align: center;
    color: #2e7d32;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    font-weight: 600;
  }

  .trainers-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 1rem 0;
  }

  @media (max-width: 768px) {
    .trainers-container {
      padding: 1rem 0.5rem;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 2rem;
    }

    .trainers-grid {
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
    }
  }

  @media (max-width: 480px) {
    .trainers-grid {
      grid-template-columns: 1fr;
      gap: 1rem;
    }
  }
</style>
