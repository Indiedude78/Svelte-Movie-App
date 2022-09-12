<script>
	import { browser } from "$app/env";

	import defaultPic from "../../pictures/default.png";
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
	let search_type = "";

	$: searchquery = 'Searching for... "' + movie + '"';

	async function search(e) {
		e.preventDefault();
		search_results = [];
		const res = await fetch(
			"http://98.109.173.128:50014/movie-api/protected/search.php",
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

		if (data.status == "success" && data.type == "db") {
			search_type = "Database";
			data.data.movies.forEach((movie) => {
				search_results = [...search_results, movie];
			});
			console.log(search_results);
		} else {
			search_type = "API";
			console.log(data.data.movies);
			search_results = data.data.movies;

			console.log(search_type);
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
		placeholder="Search for a movie to begin"
	/>
	<button type="submit">Search</button>
</form>

{#if movie !== ""}
	<p>{searchquery}</p>
{/if}

{#if search_results.length > 0}
	<div class="movie-list">
		{#each search_results as movie}
			{#if movie.poster != "N/A" && search_type == "Database"}
				<MediaCard
					poster={movie.poster}
					title={movie.title}
					id={movie.imdb_id}
				/>
			{:else if search_type == "API" && movie.Poster != "N/A"}
				<MediaCard
					title={movie.Title}
					id={movie.imdbID}
					poster={movie.Poster}
				/>
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
		width: 100%;
		/* margin: auto; */
		flex-direction: column;
		justify-content: center;
	}
</style>
