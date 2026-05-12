<script>
  import { PUBLIC_BASE_URL } from "$env/static/public";
  import { goto } from "$app/navigation";

  let { trainer } = $props();

  // ============================================================
  // Exercise 4：点击卡片跳转到动态路由 /trainers/[trainerId]
  // 使用 goto() 导航
  // ============================================================
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

<!-- ============================================================
Exercise 4：整个卡片可点击，跳转到对应训练师详情页
路由：/trainers/[trainerId]
============================================================= -->
<div
  class="trainer-card"
  role="button"
  tabindex="0"
  onclick={handleCardClick}
  onkeydown={handleKeydown}
>
  <div class="card-image">
    <img src="{PUBLIC_BASE_URL}{trainer.image}" alt={trainer.name} />
  </div>
  <div class="card-content">
    <h3 class="trainer-name">{trainer.name}</h3>
    <p class="trainer-rank">{trainer.rank}</p>
    <p class="trainer-id">ID: {trainer.trainerId}</p>
  </div>
</div>

<style>
  .trainer-card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    overflow: hidden;
    transition: all 0.3s ease;
    cursor: pointer;
  }
  .trainer-card:hover { transform: translateY(-4px); box-shadow: 0 8px 25px rgba(0,0,0,0.15); }
</style>