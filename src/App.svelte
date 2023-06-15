<script lang="ts">
  import Team from './lib/Team.svelte'
  import TeamWon from './lib/TeamWon.svelte';

  let isButtonDisabled: boolean;
  let teamPoints: number;
  let winner: 'blue' | 'red' | null = null;
  $: redPoints = teamPoints;
  $: bluePoints = teamPoints;

  function onUpdatePoints(e) {
    const { teamPoints: currentPoints, color: currentColor } = e.detail;

    if (currentPoints === 0) {
      isButtonDisabled = true;
      
      if (currentColor === 'blue') {
        winner = 'red';
      } else if (currentColor === 'red') {
        winner = 'blue';
      } else {
        winner = null;
      }
    }
  }

  function resetGame() {
    redPoints = 20;
    bluePoints = 20;
    winner = null;
    isButtonDisabled = false;
  }
</script>

<main>
  <div class="pb-8">
    <h1 class="h1">MTG Counter App</h1>
  </div>

  <div class="card w-full grid grid-cols-3 gap-4 place-items-center">
    <Team color="red" bind:teamPoints={redPoints} {isButtonDisabled} on:update_points={onUpdatePoints} />
    <span class="divider-vertical h-20"></span>
    <Team color="blue" bind:teamPoints={bluePoints} {isButtonDisabled} on:update_points={onUpdatePoints} /> 
  </div>
  {#if winner}
  <div class="w-full grid p-5">
    <TeamWon {winner} />
  </div>
  {/if}
  <button class="m-8" on:click={resetGame}>Reset Game</button>
</main>
