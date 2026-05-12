<script>
  // 引入环境变量（API 基础地址）
  import { PUBLIC_BASE_URL } from "$env/static/public";

  // 题目要求：使用 onMount() 生命周期函数
  import { onMount } from "svelte";

  // 加载组件
  import LoadingSpinner from "$lib/components/LoadingSpinner.svelte";
  import TrainerCard from "$lib/components/TrainerCard.svelte";

  // 响应式数据：存储所有训练师列表
  let trainers = $state([]);
  let loading = $state(true);
  let error = $state(null);

  // ======================================================
  // Exercise 3 要求：
  // 使用 fetch()、async 函数、onMount() 从 API 加载训练师数据
  // API 地址：https://pkserve.ocean.anhydrous.dev/api/trainers
  // ======================================================
  onMount(async () => {
    try {
      // 题目要求：使用 fetch() 获取数据
      const res = await fetch(`${PUBLIC_BASE_URL}/api/trainers`);

      if (!res.ok) throw new Error("Failed to fetch trainers");

      // 解析 JSON 数据
      const data = await res.json();

      // 更新数据
      trainers = data;
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  });
</script>

<!-- ======================================================
Exercise 3：页面标题
====================================================== -->
<svelte:head>
  <title>Trainer Database</title>
</svelte:head>

<div class="trainers-container">
  <h1>Pokémon Trainer Database</h1>

  <!-- 加载状态 -->
  {#if loading}
    <LoadingSpinner text="Loading trainers..." />
  {:else if error}
    <p class="error">Error: {error}</p>
  {:else}
    <div class="trainers-grid">
      <!-- 渲染所有训练师 -->
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
  }

  .trainers-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .error {
    color: red;
    text-align: center;
    font-size: 1.2rem;
  }
</style>