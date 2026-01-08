<script>
  // State management tanpa useState atau setState
  let count = 0;

  // Reactive statement - otomatis re-run ketika count berubah
  $: doubleCount = count * 2;
  
  // Reactive statement untuk side effect
  $: if (count > 10) {
    console.log('Count is getting high!');
  }

  // Pure functions
  function increment() {
    count += 1; // Langsung assign, auto reactive!
  }

  function decrement() {
    count -= 1;
  }

  function reset() {
    count = 0;
  }
</script>

<div class="counter">
  <div class="display">
    <div class="count-value">{count}</div>
    <div class="double-value">Double: {doubleCount}</div>
  </div>

  <div class="buttons">
    <button on:click={decrement}>−</button>
    <button on:click={reset}>Reset</button>
    <button on:click={increment}>+</button>
  </div>

  {#if count > 10}
    <div class="warning">⚠️ Count is high!</div>
  {/if}
</div>

<style>
  .counter {
    text-align: center;
  }

  .display {
    margin-bottom: 1.5rem;
  }

  .count-value {
    font-size: 4rem;
    font-weight: bold;
    color: #4CAF50;
  }

  .double-value {
    font-size: 1.2rem;
    color: #666;
    margin-top: 0.5rem;
  }

  .buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
  }

  button {
    padding: 0.8rem 1.5rem;
    font-size: 1.2rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background: #4CAF50;
    color: white;
    transition: background 0.2s;
  }

  button:hover {
    background: #45a049;
  }

  button:active {
    transform: scale(0.95);
  }

  .warning {
    margin-top: 1rem;
    padding: 0.5rem;
    background: #fff3cd;
    color: #856404;
    border-radius: 4px;
  }
</style>