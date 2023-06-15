<script lang="ts">
    import { createEventDispatcher } from "svelte";
    export let teamPoints = 20;
    export let color: 'blue' | 'red';
    export let isButtonDisabled = false;

    const dispatch = createEventDispatcher();

    let textColor;
    if (color === 'blue') {
        textColor = 'text-blue-400';
    } else if (color === 'red') {
        textColor = 'text-red-400';
    }

    function onSubtractPoints(e) {
        if (teamPoints !== 0) {
            teamPoints -= 1;
        }

        dispatch('update_points', {
            teamPoints,
            color,
        });
    }

    function onAddPoints(e) {
        teamPoints += 1;

        dispatch('update_points', {
            teamPoints,
        });
    }
</script>
<div class="bg-white p-8 rounded-md">
    <h3 class="h3 pb-4 capitalize {textColor} font-bold">Team {color}: {teamPoints}</h3>
    {#if isButtonDisabled}
        <button type="button" class="btn-sm bg-green-500 hover:bg-green-600" on:click={onAddPoints} disabled>+</button>
        <button type="button" class="btn-sm bg-red-500 hover:bg-red-600 m-2" on:click={onSubtractPoints} disabled>-</button>
    {:else}
        <button type="button" class="btn-sm bg-green-500 hover:bg-green-600" on:click={onAddPoints}>+</button>
        <button type="button" class="btn-sm bg-red-500 hover:bg-red-600 m-2" on:click={onSubtractPoints}>-</button>
    {/if}
</div>
