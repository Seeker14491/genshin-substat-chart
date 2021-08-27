<script>
	import Chart from "./Chart.svelte";
	import { substatData } from "./data";
</script>

{#each substatData as sd}
	<Chart substatData={sd} />
{/each}
