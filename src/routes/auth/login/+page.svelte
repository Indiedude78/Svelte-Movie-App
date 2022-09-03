<script>
	let username = "";
	let password = "";
	let message;
	import { browser } from "$app/env";
	if (browser) {
		if (localStorage.getItem("user")) {
			window.location.href = "/";
		}
	}
	async function login(e) {
		e.preventDefault();
		const res = await fetch(
			"http://98.109.173.128:50014/movie-api/user/login.php",
			{
				method: "POST",
				headers: {
					"Content-Type": "application/json",
				},
				body: JSON.stringify({
					username,
					password,
				}),
			}
		);
		const data = await res.json();
		if (data) {
			console.log(data);
			if (browser && data.jwt) {
				localStorage.setItem("user", data.jwt);
				console.log(localStorage.getItem("user"));
				window.location.href = "/home";
			} else if (browser && !data.jwt) {
				message = data.error;
			}
		} else {
			console.log("error");
		}

		password = "";
	}
</script>

<h1>Log In</h1>
<form method="post">
	<div class="form-group">
		<label for="username">Username</label>
		<input
			type="text"
			class="form-control"
			id="email"
			aria-describedby="emailHelp"
			placeholder="Enter username"
			bind:value={username}
		/>
	</div>
	<div class="form-group">
		<label for="password">Password</label>
		<input
			type="password"
			class="form-control"
			id="password"
			placeholder="Password"
			bind:value={password}
		/>
	</div>

	<input
		type="submit"
		on:click|preventDefault={login}
		class="btn btn-primary"
		value="Submit"
		disabled={username == "" || password == ""}
	/>
</form>
{#if message}
	<pre>{message}</pre>
{/if}

<style>
	form {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	form .form-group {
		margin: 0.5rem;
	}
	form .form-group input {
		width: 100%;
	}
	form .form-group label {
		font-size: 1.2rem;
		font-weight: bold;
		text-transform: uppercase;
	}
	form .form-group {
		margin-top: 0.5rem;
	}
</style>
