<script>
	let email = '';
	let password = '';
	let message;
	async function login(e) {
		e.preventDefault();
		const res = await fetch('http://192.168.1.142/movie-api/user/register.php', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				email,
				password
			})
		});
		const data = await res.json();
		if (data.error) {
			message = 'Log in failed';
		} else {
			console.log(data.message);
			//go to the home page
			//window.location.href = '/';
		}
	}
</script>

<h1>Log In</h1>
<form method="post">
	<div class="form-group">
		<label for="email">Email</label>
		<input
			type="email"
			class="form-control"
			id="email"
			aria-describedby="emailHelp"
			placeholder="Enter email"
			bind:value={email}
		/>
		<small id="emailHelp" class="form-text text-muted"
			>We'll never share your email with anyone else.</small
		>
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
		disabled={email == '' || password == ''}
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
	form .form-group small {
		font-size: 0.8rem;
		color: #999;
	}
	form .form-group {
		margin-top: 0.5rem;
	}
</style>
