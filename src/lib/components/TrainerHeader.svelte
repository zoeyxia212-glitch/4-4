<script>
  import { PUBLIC_BASE_URL } from "$env/static/public";
  let { trainer } = $props();
</script>

<div class="trainer-header">
  <div class="trainer-image">
    <img src="{PUBLIC_BASE_URL}{trainer.image}" alt={trainer.name} />
  </div>
  <div class="trainer-info">
    <h1 class="trainer-name">{trainer.name}</h1>
    <p class="trainer-rank">{trainer.rank}</p>
    <p class="trainer-id">Trainer ID: {trainer.trainerId}</p>
    <a href="/trainers" class="back-link">← Back to Trainers</a>
  </div>
</div>

<style>
  .trainer-header {
    display: flex;
    gap: 3rem;
    margin-bottom: 4rem;
    padding: 2rem;
    background: white;
    border-radius: 16px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  }
</style>