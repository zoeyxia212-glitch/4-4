<script>
  // 引入全局样式
  import "$lib/css/app.css";
  // 引入自定义导航栏组件（Exercise 2 要求：创建全局共享 navbar）
  import Navbar from "$lib/components/Navbar.svelte";

  // SvelteKit 内置对象：获取当前页面 URL 信息，用于导航高亮
  import { page } from "$app/state";

  // Svelte 5 语法：接收子页面内容（必须写，否则页面无法渲染）
  let { children } = $props();
  // 响应式跟踪当前路径，用于导航栏判断活跃状态
  let path = $derived(page.url.pathname);
</script>

<!-- 全局导航栏：所有页面都会显示（Exercise 2 核心要求） -->
<Navbar />

<!-- 页面容器：子页面内容渲染位置 -->
<div class="container">
  {@render children()}
</div>

<style>
  .container {
    width: 1200px;
    margin: 0 auto;

    @media (max-width: 1200px) {
      width: 100%;
    }
  }
</style>