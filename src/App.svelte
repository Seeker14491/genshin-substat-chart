<script>
	import Chart from "./Chart.svelte";
	import { substatData } from "./data";
</script>

<div class="flex flex-col items-center py-8">
	<h1 class="text-2xl text-center">Genshin 5⭐ artifact subroll ranges</h1>
	<div class="grid xl:grid-cols-2 w-full gap-8 p-4">
		{#each substatData as sd}
			<Chart substatData={sd} />
		{/each}
	</div>
	<a href="https://github.com/Seeker14491/genshin-substat-chart" target="_blank" class="underline pt-8">GitHub</a>
</div>

<style global>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>
