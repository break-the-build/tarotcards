<!-- TarotCard.svelte -->

<script>
  export let card;
  export let isFlipped = false;
  export let onClick;

  function handleFlip() {
    onClick();
  }
</script>

<div class="max-w-sm w-64 h-auto rounded overflow-hidden shadow-lg cursor-pointer bg-gray-800 text-white" on:click={handleFlip}>
  {#if isFlipped}
    <img class="w-full h-64 object-cover" src={card.image} alt={card.name} />
    <div class="px-6 py-4 flex flex-col h-48">
      <div class="font-bold text-xl mb-2">{card.name}</div>
      <p class="text-gray-300 text-base overflow-y-auto flex-grow">{card.description}</p>
    </div>
  {:else}
    <div class="w-full h-112 bg-gray-600 flex items-center justify-center">
      <p class="text-2xl font-bold">Click to Flip</p>
    </div>
  {/if}
</div>

<style>
  .h-112 {
    height: 28rem; /* 112 * 0.25rem */
  }

  .overflow-y-auto {
    overflow-y: auto;
  }
</style>
