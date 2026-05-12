<script>
  // ==============================
  // Exercise 5 - Trainers 专属布局
  // 作用：给 /trainers 和 /trainers/[trainerId] 提供共享侧边栏
  // 不会影响首页 /about 等页面
  // ==============================

  import { onMount } from "svelte";
  import { page } from "$app/state";
  import LoadingSpinner from "$lib/components/LoadingSpinner.svelte";
  import { PUBLIC_BASE_URL } from "$env/static/public";

  // SvelteKit 布局必须接收 children（渲染子页面）
  let { children } = $props();

  // 训练师列表、加载状态、错误状态
  let trainers = $state([]);
  let loading = $state(true);
  let error = $state(null);

  // ==============================
  // Exercise 5 - 获取当前路由里的 trainerId
  // 用于侧边栏高亮当前选中的训练师
  // ==============================
  let currentTrainerId = $derived(page.params.trainerId);

  // ==============================
  // Exercise 5 - 加载所有训练师（用于侧边栏）
  // 页面一进来就请求列表
  // ==============================
  onMount(async () => {
    try {
      const response = await fetch(`${PUBLIC_BASE_URL}/api/trainers`);
      if (!response.ok) throw new Error("Failed to fetch trainers");
      trainers = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  });
</script>

<div class="trainers-layout">
  <!-- ==============================
    Exercise 5 核心：侧边栏
    所有 trainers 路由下的页面都会显示这个侧边栏
  ============================== -->
  <aside class="sidebar">
    <h2>Trainers</h2>

    {#if loading}
      <div class="sidebar-loading">
        <div class="mini-spinner"></div>
        <p>Loading...</p>
      </div>
    {:else if error}
      <p class="error">Failed to load trainers</p>
    {:else if trainers.length > 0}
      <nav class="trainer-nav">
        <ul>
          <!-- 循环显示所有训练师 -->
          {#each trainers as trainer}
            <li>
              <!-- 
                ==============================
                ✅ a 标签正确闭合 >
                ✅ 高亮条件正确
                ==============================
              -->
              <a
                href="/trainers/{trainer.trainerId}"
                class="trainer-link"
                class:active={currentTrainerId === trainer.trainerId}
              >
                <div class="trainer-info">
                  <span class="trainer-name">{trainer.name}</span>
                  <span class="trainer-rank">{trainer.rank}</span>
                </div>
              </a>
            </li>
          {/each}
        </ul>
      </nav>
    {:else}
      <p class="no-trainers">No trainers found</p>
    {/if}
  </aside>

  <!-- 子页面内容渲染位置 -->
  <main class="main-content">
    {@render children()}
  </main>
</div>

<style>
  .trainers-layout {
    display: flex;
    min-height: calc(100vh - 120px);
    gap: 2rem;
    max-width: 1400px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .sidebar {
    width: 300px;
    flex-shrink: 0;
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    padding: 2rem;
    height: fit-content;
    position: sticky;
    top: 5rem;
  }

  .sidebar h2 {
    color: #2e7d32;
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0 0 1.5rem 0;
    text-align: center;
    border-bottom: 2px solid #e8f5e8;
    padding-bottom: 0.75rem;
  }

  .sidebar-loading {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    padding: 2rem 0;
  }

  .mini-spinner {
    width: 20px;
    height: 20px;
    border: 2px solid #e0e0e0;
    border-top: 2px solid #4caf50;
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  .sidebar-loading p {
    color: #666;
    font-size: 0.9rem;
    margin: 0;
  }

  .error, .no-trainers {
    color: #666;
    font-style: italic;
    text-align: center;
    padding: 1rem 0;
    margin: 0;
  }

  .error {
    color: #d32f2f;
  }

  .trainer-nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .trainer-nav li {
    margin-bottom: 0.5rem;
  }

  .trainer-link {
    display: block;
    padding: 1rem;
    border-radius: 8px;
    text-decoration: none;
    color: inherit;
    transition: all 0.2s ease;
    border: 2px solid transparent;
  }

  .trainer-link:hover {
    background: #f8f9fa;
    border-color: #e8f5e8;
    transform: translateX(4px);
  }

  .trainer-link.active {
    background: #e8f5e8;
    border-color: #4caf50;
    box-shadow: 0 2px 8px rgba(76, 175, 80, 0.2);
  }

  .trainer-info {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }

  .trainer-name {
    font-weight: 600;
    color: #2e7d32;
    font-size: 1rem;
  }

  .trainer-rank {
    font-size: 0.85rem;
    color: #4caf50;
    font-weight: 500;
  }

  .main-content {
    flex: 1;
    min-width: 0;
  }

  @media (max-width: 1024px) {
    .trainers-layout {
      flex-direction: column;
      padding: 1rem 0.5rem;
    }

    .sidebar {
      width: 100%;
      position: static;
      margin-bottom: 2rem;
    }
  }
</style>