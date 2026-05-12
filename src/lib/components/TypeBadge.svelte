<script>
  // ==============================
  // Exercise 4 - 宝可梦属性标签组件
  // 接收从 PokemonCard 传入的属性类型（type）
  // 例如: Grass, Fire, Water, Poison 等
  // ==============================
  let { type } = $props();
</script>

<!-- ==============================
  Exercise 4 要求：显示宝可梦属性
  动态设置 CSS 类名，实现不同属性不同颜色
============================== -->
<span class="type-badge type-{type.toLowerCase()}">{type}</span>

<style>
  /* 基础样式：所有属性标签共用 */
  .type-badge {
    padding: 0.25rem 0.75rem;
    border-radius: 16px;
    font-size: 0.8rem;
    font-weight: 600;
    text-transform: uppercase;
    color: white;
    letter-spacing: 0.5px;
  }

  /* ==============================
    Exercise 4 - 宝可梦全属性配色
    对应不同属性显示不同颜色
  ============================== */
  .type-normal {
    background: #a8a878;
  }
  .type-fire {
    background: #f08030;
  }
  .type-water {
    background: #6890f0;
  }
  .type-electric {
    background: #f8d030;
    color: #333;
  }
  .type-grass {
    background: #78c850;
  }
  .type-ice {
    background: #98d8d8;
  }
  .type-fighting {
    background: #c03028;
  }
  .type-poison {
    background: #a040a0;
  }
  .type-ground {
    background: #e0c068;
    color: #333;
  }
  .type-flying {
    background: #a890f0;
  }
  .type-psychic {
    background: #f85888;
  }
  .type-bug {
    background: #a8b820;
  }
  .type-rock {
    background: #b8a038;
  }
  .type-ghost {
    background: #705898;
  }
  .type-dragon {
    background: #7038f8;
  }
  .type-dark {
    background: #705848;
  }
  .type-steel {
    background: #b8b8d0;
    color: #333;
  }
  .type-fairy {
    background: #ee99ac;
    color: #333;
  }
</style>