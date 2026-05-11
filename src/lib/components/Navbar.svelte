<script>
  import { page } from "$app/state";
  let path = $derived(page.url.pathname);
</script>

<!-- Material UI style navbar with green color scheme -->
<nav class="navbar">
  <div class="nav-container">
    <div class="nav-brand">
      <a href="/" class="brand-link">CS719 Lab - Svelte IV</a>
    </div>
    <div class="nav-links">
      <a href="/" class="nav-link" class:active={path === "/"}> Home </a>
      <a href="/about" class="nav-link" class:active={path.startsWith("/about")}> About Me </a>
      <a href="/trainers" class="nav-link" class:active={path.startsWith("/trainers")}>
        Trainer Database
      </a>
    </div>
  </div>
</nav>

<style>
  /* Material UI style navbar with green color scheme */
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

  .nav-brand .brand-link {
    color: white;
    font-size: 1.5rem;
    font-weight: 600;
    text-decoration: none;
    letter-spacing: 0.5px;
  }

  .nav-brand .brand-link:hover {
    color: #e8f5e8;
  }

  .nav-links {
    display: flex;
    gap: 0.5rem;
  }

  .nav-link {
    color: white;
    text-decoration: none;
    padding: 0.75rem 1.5rem;
    border-radius: 4px;
    font-weight: 500;
    transition: all 0.2s ease-in-out;
    position: relative;
  }

  .nav-link:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateY(-1px);
  }

  .nav-link.active {
    background: rgba(255, 255, 255, 0.2);
    color: #e8f5e8;
    font-weight: 600;
  }

  .nav-link.active::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 80%;
    height: 2px;
    background: white;
    border-radius: 1px;
  }

  @media (max-width: 768px) {
    .nav-container {
      flex-direction: column;
      height: auto;
      padding: 1rem;
      gap: 1rem;
    }

    .nav-links {
      width: 100%;
      justify-content: center;
    }

    .nav-link {
      padding: 0.5rem 1rem;
    }
  }
</style>
