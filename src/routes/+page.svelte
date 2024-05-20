<!-- src/routes/+page.svelte -->

<script>
  import { onMount } from 'svelte';
  import { tarotCards } from '$lib/data/tarotCards';
  import TarotCard from '$lib/components/TarotCard.svelte';

  let drawnCards = [];
  let flippedStates = [false, false, false];
  let isMobile = false;

  function pickThreeCards() {
    const shuffled = tarotCards.sort(() => 0.5 - Math.random());
    drawnCards = shuffled.slice(0, 3);
    flippedStates = [false, false, false];
  }

  function flipCard(index) {
    flippedStates[index] = true;
    flippedStates = [...flippedStates];
  }

  function checkIsMobile() {
    isMobile = window.innerWidth <= 768;
  }

  onMount(() => {
    pickThreeCards();
    checkIsMobile();
    window.addEventListener('resize', checkIsMobile);
    return () => window.removeEventListener('resize', checkIsMobile);
  });
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
  <h1 class="text-4xl font-bold mb-8">Tarot Card Reader</h1>

  {#if isMobile}
    <div class="w-full max-w-md flex flex-col items-center">
      {#each drawnCards as card, index}
        <div class="mb-4 w-full flex justify-center">
          <div class="text-center">
            <h2 class="text-xl font-semibold mb-2">{index === 0 ? 'Past' : index === 1 ? 'Present' : 'Future'}</h2>
            <TarotCard card={card} isFlipped={flippedStates[index]} onClick={() => flipCard(index)} />
          </div>
        </div>
      {/each}
    </div>
  {:else}
    <div class="flex space-x-4">
      {#if drawnCards.length === 3}
        <div>
          <h2 class="text-xl font-semibold mb-2">Past</h2>
          <TarotCard card={drawnCards[0]} isFlipped={flippedStates[0]} onClick={() => flipCard(0)} />
        </div>
        <div>
          <h2 class="text-xl font-semibold mb-2">Present</h2>
          <TarotCard card={drawnCards[1]} isFlipped={flippedStates[1]} onClick={() => flipCard(1)} />
        </div>
        <div>
          <h2 class="text-xl font-semibold mb-2">Future</h2>
          <TarotCard card={drawnCards[2]} isFlipped={flippedStates[2]} onClick={() => flipCard(2)} />
        </div>
      {/if}
    </div>
  {/if}
  
  <button on:click={pickThreeCards} class="mt-8 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700">
    Draw Another Set of Cards
  </button>
</div>
