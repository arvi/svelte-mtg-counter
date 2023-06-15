<script lang="ts">
    export let winner: 'blue' | 'red';

    // tailwind cannot recognize dynamically generated class name e.g bg-{bgColor}-500
    let bgColor;
    if (winner === 'blue') {
        bgColor = 'bg-blue-500';
    } else if (winner === 'red') {
        bgColor = 'bg-red-500';
    }
</script>

<div class="{bgColor} p-4 mt-4 rounded-md">
    <h3 class="h3 pb-2 capitalize font-bold">{winner} Won!</h3>
</div>
