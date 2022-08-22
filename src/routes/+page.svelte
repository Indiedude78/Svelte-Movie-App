<script>
	import Card from '../components/mediacard.svelte';
	const count = Array(10).fill(0);
</script>
<svelte:head>
	<title>Watch with me</title>
</svelte:head>
<h1>Watch Movies Together</h1>
<div class="movie-list">
	{#each count as i}
		<Card />
	{/each}
</div>

<style>
	.movie-list {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		flex-wrap: wrap;
	}
</style>
