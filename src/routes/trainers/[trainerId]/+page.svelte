<script>
  // ==============================
  // Exercise 4: 训练师详情页（动态路由）
  // 路由：/trainers/[trainerId]
  // ==============================

  import { PUBLIC_BASE_URL } from "$env/static/public";
  import { page } from "$app/state";
  import LoadingSpinner from "$lib/components/LoadingSpinner.svelte";
  import TrainerHeader from "$lib/components/TrainerHeader.svelte";
  import PokemonCard from "$lib/components/PokemonCard.svelte";

  // 响应式状态
  let trainer = $state(null);
  let loading = $state(true);
  let error = $state(null);

  // 从路由获取 trainerId
  let trainerId = $derived(page.params.trainerId);

  // ==============================
  // ✅ 正确写法：$effect 不需要 import！
  // 监听 trainerId 变化，重新获取详情
  // ==============================
  $effect(() => {
    async function fetchTrainer() {
      try {
        loading = true;
        const res = await fetch(`${PUBLIC_BASE_URL}/api/trainers/${trainerId}`);
        if (!res.ok) throw new Error("Trainer not found");
        trainer = await res.json();
      } catch (e) {
        error = e.message;
      } finally {
        loading = false;
      }
    }
    fetchTrainer();
  });
</script>

<svelte:head>
  <title>{trainer ? trainer.name : 'Trainer Details'}</title>
</svelte:head>

<div class="detail-page">
  {#if loading}
    <LoadingSpinner />
  {:else if error}
    <div class="error-box">
      <h2>❌ {error}</h2>
      <a href="/trainers">← Back to trainers</a>
    </div>
  {:else if trainer}
    <TrainerHeader {trainer} />

    <div class="team-section">
      <h2>{trainer.name}'s Team</h2>
      <div class="pokemon-grid">
        {#each trainer.pokemon as pkm}
          <PokemonCard pokemon={pkm} />
        {/each}
      </div>
    </div>
  {/if}
</div>

<style>
  .detail-page {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  .team-section h2 {
    color: #2e7d32;
    font-size: 2rem;
    margin: 3rem 0 2rem 0;
    text-align: center;
  }

  .pokemon-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1.5rem;
  }

  .error-box {
    text-align: center;
    padding: 3rem;
    background: #ffebee;
    border-radius: 12px;
  }

  .error-box a {
    color: #4caf50;
    text-decoration: none;
    font-weight: bold;
  }
</style>