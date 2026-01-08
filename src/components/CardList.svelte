<script>
  // Data array
  let cards = [
    { id: 1, title: 'Reactive', emoji: '⚡', description: 'Auto-update UI' },
    { id: 2, title: 'Compiled', emoji: '🔨', description: 'No runtime overhead' },
    { id: 3, title: 'Minimal', emoji: '🎯', description: 'Less boilerplate' },
  ];

  let newTitle = '';
  let newEmoji = '';
  let newDescription = '';

  // Reactive computed value
  $: cardCount = cards.length;
  $: isEmpty = cards.length === 0;

  function addCard() {
    if (newTitle && newEmoji) {
      cards = [...cards, {
        id: Date.now(),
        title: newTitle,
        emoji: newEmoji,
        description: newDescription || 'No description'
      }];
      
      // Reset form
      newTitle = '';
      newEmoji = '';
      newDescription = '';
    }
  }

  function removeCard(id) {
    cards = cards.filter(card => card.id !== id);
  }
</script>

<div class="card-list">
  <div class="stats">
    Total Cards: <strong>{cardCount}</strong>
  </div>

  <div class="form">
    <input 
      type="text" 
      bind:value={newTitle} 
      placeholder="Title"
    />
    <input 
      type="text" 
      bind:value={newEmoji} 
      placeholder="Emoji"
      maxlength="2"
    />
    <input 
      type="text" 
      bind:value={newDescription} 
      placeholder="Description"
    />
    <button on:click={addCard}>Add Card</button>
  </div>

  {#if isEmpty}
    <p class="empty">No cards yet. Add one!</p>
  {:else}
    <div class="cards">
      {#each cards as card (card.id)}
        <div class="item">
          <div class="emoji">{card.emoji}</div>
          <div class="content">
            <h3>{card.title}</h3>
            <p>{card.description}</p>
          </div>
          <button 
            class="remove" 
            on:click={() => removeCard(card.id)}
          >
            ✕
          </button>
        </div>
      {/each}
    </div>
  {/if}
</div>

<style>
  .card-list {
    width: 100%;
  }

  .stats {
    margin-bottom: 1rem;
    font-size: 1.1rem;
    color: #666;
  }

  .form {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
  }

  input {
    padding: 0.6rem;
    border: 2px solid #ddd;
    border-radius: 6px;
    font-size: 1rem;
  }

  input:focus {
    outline: none;
    border-color: #4CAF50;
  }

  button {
    padding: 0.8rem;
    background: #4CAF50;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 500;
  }

  button:hover {
    background: #45a049;
  }

  .empty {
    text-align: center;
    color: #999;
    padding: 2rem;
  }

  .cards {
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
  }

  .item {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
    background: #f9f9f9;
    border-radius: 8px;
    transition: transform 0.2s;
  }

  .item:hover {
    transform: translateX(5px);
  }

  .emoji {
    font-size: 2rem;
  }

  .content {
    flex: 1;
  }

  .content h3 {
    margin: 0 0 0.3rem 0;
    font-size: 1.1rem;
  }

  .content p {
    margin: 0;
    color: #666;
    font-size: 0.9rem;
  }

  .remove {
    background: #f44336;
    padding: 0.4rem 0.8rem;
    font-size: 0.9rem;
  }

  .remove:hover {
    background: #da190b;
  }
</style>