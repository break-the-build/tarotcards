<script>
  import { tarotCards } from '$lib/data/tarotCards';
  import TarotCard from '$lib/components/TarotCard.svelte';

  let drawnCards = [];
  let flippedStates = [false, false, false];

  function pickThreeCards() {
    const shuffled = tarotCards.sort(() => 0.5 - Math.random());
    drawnCards = shuffled.slice(0, 3);
    flippedStates = [false, false, false];
  }

  function flipCard(index) {
    flippedStates[index] = true;
    flippedStates = [...flippedStates];
  }

  pickThreeCards();
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
  <h1 class="text-4xl font-bold mb-8">Tarot Card Reader</h1>
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
  <button on:click={pickThreeCards} class="mt-8 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700">
    Draw Another Set of Cards
  </button>
</div>
