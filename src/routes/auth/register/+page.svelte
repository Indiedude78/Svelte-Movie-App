<script>
	let firstname = '',
		lastname = '',
		email = '',
		username = '',
		password = '',
		confirm_password = '';
	let return_msg;
	let pass_msg = '';

	$: pass_match = () => {
		if (password == confirm_password) {
			pass_msg = 'Passwords match';
		} else {
			pass_msg = 'Passwords do not match';
		}
	};

	async function register(e) {
		e.preventDefault();
		e.preventDefault();
		const res = await fetch('http://192.168.1.142/movie-api/user/register.php', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({
				firstname,
				lastname,
				email,
				username,
				password,
				confirm_password
			})
		});
		const data = await res.json();

		console.log(data);
		if (data.error) {
			return_msg = data.error;
		} else {
			return_msg = data.success;
			//set form values to empty strings
			firstname = '';
			lastname = '';
			email = '';
			username = '';
			password = '';
			confirm_password = '';
		}
	}
</script>

<h1>Register</h1>

<form method="post" on:submit|preventDefault={register}>
	<input type="text" id="fname" name="firstname" placeholder="First name" bind:value={firstname} />
	<input type="text" id="lname" name="lastname" placeholder="Last name" bind:value={lastname} />
	<input type="email" id="email" name="email" placeholder="Email" bind:value={email} />
	<input type="text" id="username" name="username" placeholder="Username" bind:value={username} />
	<input
		type="password"
		id="password"
		name="password"
		placeholder="Password"
		bind:value={password}
	/>
	<input
		type="password"
		id="confirm_password"
		name="confirm_password"
		placeholder="Confirm Password"
		bind:value={confirm_password}
		on:input={pass_match}
	/>
	<button
		type="submit"
		class="btn btn-primary"
		disabled={firstname == '' ||
			lastname == '' ||
			email == '' ||
			username == '' ||
			password == '' ||
			confirm_password == ''}
	>
		Submit
	</button>
</form>
{#if pass_msg != '' && !return_msg}
	<pre>{pass_msg}</pre>
{/if}

{#if return_msg}
	<div class="alert alert-danger" role="alert">
		<p>{return_msg} Please <a href="/auth/login">Log In</a></p>
	</div>
{/if}

<style>
	form {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	input {
		margin: 10px;
	}
	button {
		margin: 10px;
	}
</style>
