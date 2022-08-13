<script>
	let movie = '';

	$: searchquery = 'User searched for ' + movie;
</script>

<svelte:head>
	<title>Search for movies</title>
</svelte:head>
<h1>Search</h1>
<!-- Create a form text input-->
<form method="get">
	<input type="text" bind:value={movie} name="search" id="search" autocomplete="off" />
	<input type="button" value="Search" />
</form>

{#if movie !== ''}
	<p>{searchquery}</p>
{/if}
<p />

<style>
	form {
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 1rem;
	}
	input[type='text'] {
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

	input[type='button'] {
		border: 1px solid #000;
		border-radius: 8px;
		padding: 0.5rem;
		margin: 0.5rem;
	}

	input[type='button']:hover {
		background-color: #fff;
		color: #f00;
		cursor: pointer;
	}
</style>
