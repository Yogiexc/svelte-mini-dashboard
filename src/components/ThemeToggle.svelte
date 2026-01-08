<script>
  import { createEventDispatcher, onMount } from 'svelte';

  const dispatch = createEventDispatcher();
  let isDark = false;

  onMount(() => {
    const saved = localStorage.getItem('theme');
    if (saved === 'dark') {
      isDark = true;
      dispatch('themeChange', { isDark: true });
    }
  });

  function handleToggle() {
    isDark = !isDark;
    localStorage.setItem('theme', isDark ? 'dark' : 'light');
    dispatch('themeChange', { isDark });
  }
</script>

<div class="theme-toggle">
  <label class="switch">
    <input 
      type="checkbox" 
      bind:checked={isDark}
      on:change={handleToggle}
    />
    <span class="slider">
      <span class="icon">{isDark ? '🌙' : '☀️'}</span>
    </span>
  </label>
  <span class="label">
    {isDark ? 'Dark Mode' : 'Light Mode'}
  </span>
</div>

<style>
  .theme-toggle {
    display: inline-flex;
    align-items: center;
    gap: 1rem;
    margin: 1rem 0;
  }

  .label {
    font-weight: 500;
  }

  .switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }

  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    transition: 0.4s;
    border-radius: 34px;
    display: flex;
    align-items: center;
    padding: 0 5px;
  }

  .icon {
    font-size: 1.2rem;
    transition: transform 0.4s;
  }

  input:checked + .slider {
    background-color: #2196F3;
  }

  input:checked + .slider .icon {
    transform: translateX(26px);
  }
</style>