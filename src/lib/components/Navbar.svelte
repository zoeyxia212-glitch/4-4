<script>
  import { page } from "$app/state";
  let path = $derived(page.url.pathname);
</script>

<nav class="navbar">
  <div class="nav-container">
    <div class="nav-brand">
      <a href="/" class="brand-link">CS719 Lab - Svelte IV</a>
    </div>
    <div class="nav-links">
      <!-- Exercise 2：条件样式 - 首页链接高亮 -->
      <a href="/" class="nav-link" class:active={path === "/"}> Home </a>
      
      <!-- Exercise 1 / Exercise 2：About 页面链接 + 条件高亮 -->
      <a href="/about" class="nav-link" class:active={path.startsWith("/about")}> About Me </a>
      
      <!-- Exercise 3：新增 trainers 页面导航链接 + 条件高亮 -->
      <a href="/trainers" class="nav-link" class:active={path.startsWith("/trainers")}>
        Trainer Database
      </a>
    </div>
  </div>
</nav>

<style>
  .navbar {
    background: linear-gradient(135deg, #4caf50 0%, #2e7d32 100%);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    position: sticky;
    top: 0;
    z-index: 1000;
    margin-bottom: 2rem;
  }
  .nav-container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 1rem;
    height: 64px;
  }
  .nav-brand .brand-link { color: white; font-size: 1.5rem; font-weight: 600; text-decoration: none; }
  .nav-links { display: flex; gap: 0.5rem; }
  .nav-link { color: white; text-decoration: none; padding: 0.75rem 1.5rem; border-radius: 4px; font-weight: 500; transition: all 0.2s; }
  .nav-link.active { background: rgba(255,255,255,0.2); font-weight: 600; }
</style>