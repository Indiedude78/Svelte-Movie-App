<script>
	//set poster to default if no poster is available
	export let poster = "https://via.placeholder.com/300";
	export let title;
	export let id;
</script>

<div class="card">
	<div class="card-container">
		<figure class="image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img src={poster} alt={title} />
			<div class="media-content">
				<p class="title is-4">{title}</p>
				<p class="hide">{id}</p>
			</div>
		</figure>
	</div>
</div>

<style>
	.card {
		margin: 1rem;
		text-align: center;
		display: flex;
	}
	.card-container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.card:hover {
		box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
		/*
		rotate based on mouse position
		*/
		transform: matrix(1, 0, 0, 1, 0, 0);
	}
	.hide {
		display: none;
	}
</style>
