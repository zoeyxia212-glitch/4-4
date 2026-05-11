<script>
  import { PUBLIC_BASE_URL } from "$env/static/public";
  import { goto } from "$app/navigation";

  let { trainer } = $props();

  function handleCardClick() {
    goto(`/trainers/${trainer.trainerId}`);
  }

  function handleKeydown(event) {
    if (event.key === "Enter" || event.key === " ") {
      event.preventDefault();
      goto(`/trainers/${trainer.trainerId}`);
    }
  }
</script>

<div
  class="trainer-card"
  role="button"
  tabindex="0"
  aria-label="View details for {trainer.name}"
  onclick={handleCardClick}
  onkeydown={handleKeydown}
>
  <div class="card-image">
    <img src="{PUBLIC_BASE_URL}{trainer.image}" alt={trainer.name} loading="lazy" />
  </div>
  <div class="card-content">
    <h3 class="trainer-name">{trainer.name}</h3>
    <p class="trainer-rank">{trainer.rank}</p>
    <p class="trainer-id">ID: {trainer.trainerId}</p>
    <!-- Hidden link for semantic navigation and SEO -->
    <a href="/trainers/{trainer.trainerId}" class="sr-only">View {trainer.name} details</a>
  </div>
</div>

<style>
  .trainer-card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: all 0.3s ease;
    position: relative;
    cursor: pointer;
  }

  .trainer-card:focus {
    outline: 2px solid #4caf50;
    outline-offset: 2px;
  }

  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
  }

  .trainer-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  }

  .card-image {
    width: 100%;
    height: 250px;
    overflow: hidden;
    background: linear-gradient(45deg, #f5f5f5, #e8f5e8);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .card-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .trainer-card:hover .card-image img {
    transform: scale(1.05);
  }

  .card-content {
    padding: 1.5rem;
  }

  .trainer-name {
    margin: 0 0 0.5rem 0;
    color: #2e7d32;
    font-size: 1.5rem;
    font-weight: 600;
    line-height: 1.2;
  }

  .trainer-rank {
    margin: 0 0 1rem 0;
    color: #4caf50;
    font-size: 1.1rem;
    font-weight: 500;
    padding: 0.25rem 0.75rem;
    background: #e8f5e8;
    border-radius: 20px;
    display: inline-block;
  }

  .trainer-id {
    margin: 0;
    color: #757575;
    font-size: 0.9rem;
    font-weight: 500;
    letter-spacing: 0.5px;
  }

  @media (max-width: 768px) {
    .card-content {
      padding: 1rem;
    }

    .trainer-name {
      font-size: 1.3rem;
    }
  }
</style>
