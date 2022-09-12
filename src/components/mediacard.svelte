<script>
	import { goto } from "$app/navigation";
	//set poster to default if no poster is available
	export let poster = "https://via.placeholder.com/300";
	export let title;
	export let id;
</script>

<div class="card">
	<div class="card-side front card-container">
		<figure class="image">
			<!-- svelte-ignore a11y-img-redundant-alt -->
			<img src={poster} alt={title} />
			<div class="media-content">
				<p class="title is-4">{title}</p>
				<p class="hide">{id}</p>
			</div>
		</figure>
	</div>
	<div class="card-side back">
		<button>Add to watchlist</button>
		<button
			on:click={() => {
				goto("/movie/" + id);
			}}
		>
			View
		</button>
	</div>
</div>

<style>
	.card {
		perspective: 150rem;
		position: relative;
		height: 40rem;
		width: auto;
		margin: 2rem;
		box-shadow: none;
		background: none;
	}

	.card-side {
		height: 35rem;
		border-radius: 15px;
		transition: all 0.8s ease;
		backface-visibility: hidden;
		position: absolute;
		top: 0;
		left: 0;
		width: 80%;
		padding: 2rem;
		color: white;
	}
	.card-side.back {
		transform: rotateY(-180deg);
		background-color: #7b1b04;
	}
	.card-side.front {
		background-color: #262a2c;
	}

	.back {
		display: flex;
		flex-direction: column;
		justify-content: space-evenly;
	}

	.back button {
		border: none;
		border-radius: 8px;
		padding: 0.5rem;
		margin: 0.5rem;
		background-color: #fff;
		color: #f00;
	}

	.back button:hover {
		cursor: pointer;
		background-color: #f00;
		color: #fff;
	}

	.card-container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.card:hover .card-side.front {
		transform: rotateY(180deg);
	}

	.card:hover .card-side.back {
		transform: rotateY(0deg);
	}
	.hide {
		display: none;
	}
	p {
		text-align: center;
		color: black;
	}
</style>
