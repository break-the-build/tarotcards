<script>
  export let card;
  export let isFlipped = false;
  export let onClick;
</script>

<div class="max-w-sm w-64 h-96 rounded overflow-hidden shadow-lg cursor-pointer" on:click={onClick}>
  {#if isFlipped}
    <img class="w-full h-64 object-cover" src={card.image} alt={card.name} />
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{card.name}</div>
      <p class="text-gray-700 text-base">{card.description}</p>
    </div>
  {:else}
    <div class="w-full h-full bg-gray-300 flex items-center justify-center">
      <p class="text-2xl font-bold">Click to Flip</p>
    </div>
  {/if}
</div>
