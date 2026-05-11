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
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .trainer-image {
    flex-shrink: 0;
  }

  .trainer-image img {
    width: 200px;
    height: 200px;
    object-fit: cover;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .trainer-info {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .trainer-name {
    color: #2e7d32;
    font-size: 3rem;
    font-weight: 700;
    margin: 0 0 1rem 0;
    line-height: 1.1;
  }

  .trainer-rank {
    color: #4caf50;
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0 0 1rem 0;
    padding: 0.5rem 1rem;
    background: #e8f5e8;
    border-radius: 25px;
    display: inline-block;
    width: fit-content;
  }

  .trainer-id {
    color: #757575;
    font-size: 1.1rem;
    font-weight: 500;
    margin: 0 0 2rem 0;
    letter-spacing: 0.5px;
  }

  .back-link {
    color: #4caf50;
    text-decoration: none;
    font-weight: 500;
    font-size: 1.1rem;
    transition: color 0.2s ease;
  }

  .back-link:hover {
    color: #2e7d32;
    text-decoration: underline;
  }

  @media (max-width: 768px) {
    .trainer-header {
      flex-direction: column;
      text-align: center;
      gap: 2rem;
      padding: 1.5rem;
    }

    .trainer-image img {
      width: 150px;
      height: 150px;
    }

    .trainer-name {
      font-size: 2.5rem;
    }

    .trainer-rank {
      font-size: 1.3rem;
    }
  }

  @media (max-width: 480px) {
    .trainer-name {
      font-size: 2rem;
    }
  }
</style>
