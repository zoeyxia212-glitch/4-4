<script>
  let { type } = $props();
</script>

<span class="type-badge type-{type.toLowerCase()}">{type}</span>

<style>
  .type-badge {
    padding: 0.25rem 0.75rem;
    border-radius: 16px;
    font-size: 0.8rem;
    font-weight: 600;
    text-transform: uppercase;
    color: white;
    letter-spacing: 0.5px;
  }

  /* Pokemon type colors */
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
