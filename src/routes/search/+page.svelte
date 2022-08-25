<script>
	import { browser } from "$app/env";
	import MediaCard from "../../components/mediacard.svelte";
	let token;
	if (browser) {
		token = localStorage.getItem("user");
		if (!token) {
			window.location.href = "/";
		}
	}
	let movie = "";
	let search_results = [];

	$: searchquery = 'Searching for... "' + movie + '"';

	async function search(e) {
		e.preventDefault();
		search_results = [];
		const res = await fetch(
			"http://192.168.1.142/movie-api/protected/search.php",
			{
				method: "POST",
				headers: {
					"Content-Type": "application/json",
				},
				body: JSON.stringify({
					movie,
					token,
				}),
			}
		);
		const data = await res.json();
		if (data.status == "success") {
			//console.log(data.data.movies);
			data.data.movies.forEach((movie) => {
				search_results = [...search_results, movie];
			});
			console.log(search_results);
		}
	}
</script>

<svelte:head>
	<title>Search for movies</title>
</svelte:head>
<h1>Search</h1>
<!-- Create a form text input-->
<form method="post" on:submit|preventDefault={search}>
	<input
		type="text"
		bind:value={movie}
		name="search"
		id="search"
		autocomplete="off"
		placeholder="Search for a movie or a TV show"
	/>
	<button type="submit">Search</button>
</form>

{#if movie !== ""}
	<p>{searchquery}</p>
{/if}

{#if search_results.length > 0}
	<div class="movie-list">
		{#each search_results as movie}
			{#if movie.poster}
				<MediaCard
					poster={movie.poster}
					title={movie.title}
					id={movie.imdb_id}
				/>
			{:else}
				<MediaCard title={movie.title} id={movie.imdb_id} />
			{/if}
		{/each}
	</div>
	<button>Search More</button>
{/if}

<style>
	form {
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 1rem;
	}
	input[type="text"] {
		border: 1px solid #000;
		border-radius: 8px;
		padding: 0.5rem;
		margin: 0.5rem;
		width: 90%;
	}
	input:focus {
		outline: none;
		box-shadow: inset 0 0 0 1px #000;
	}

	button {
		border: 1px solid #000;
		border-radius: 8px;
		padding: 0.5rem;
		margin: 0.5rem;
	}

	button:hover {
		background-color: #fff;
		color: #f00;
		cursor: pointer;
	}
	.movie-list {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		flex-wrap: wrap;
	}
</style>
