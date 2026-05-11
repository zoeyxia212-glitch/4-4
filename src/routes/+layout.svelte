<script>
  import "$lib/css/app.css";
  import Navbar from "$lib/components/Navbar.svelte";

  // This is a special Svelte object which provides info about the current page.
  import { page } from "$app/state";

  let { children } = $props();
  let path = $derived(page.url.pathname);
</script>

<Navbar />

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
