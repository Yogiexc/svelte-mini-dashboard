<script>
  import Counter from './components/Counter.svelte';
  import ThemeToggle from './components/ThemeToggle.svelte';
  import CardList from './components/CardList.svelte';

  // State untuk dark mode
  let isDark = false;

  // Function untuk handle theme change dari child component
  function handleThemeChange(event) {
    isDark = event.detail.isDark;
  }
</script>

<main class:dark={isDark}>
  <div class="container">
    <header>
      <h1>🚀 Svelte Mini Dashboard</h1>
      <p class="subtitle">Exploring compile-time reactivity</p>
      <ThemeToggle on:themeChange={handleThemeChange} />
    </header>

    <div class="grid">
      <section class="card">
        <h2>📊 Counter Component</h2>
        <Counter />
      </section>

      <section class="card">
        <h2>🎴 Card List</h2>
        <CardList />
      </section>
    </div>
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    transition: background-color 0.3s, color 0.3s;
  }

  main {
    min-height: 100vh;
    background: #f5f5f5;
    color: #333;
    padding: 2rem;
  }

  main.dark {
    background: #1a1a1a;
    color: #f5f5f5;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  header {
    text-align: center;
    margin-bottom: 3rem;
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 0.5rem;
  }

  .subtitle {
    color: #666;
    font-size: 1.1rem;
  }

  main.dark .subtitle {
    color: #999;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .card {
    background: white;
    border-radius: 12px;
    padding: 2rem;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }

  main.dark .card {
    background: #2a2a2a;
    box-shadow: 0 2px 8px rgba(0,0,0,0.3);
  }

  h2 {
    margin-top: 0;
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
  }
</style>