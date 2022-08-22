<script>
	import AppCss from './../app.css';

	//on hover remove class
	const showDropdown = () => {
		const dropdown = document.querySelector('.dropdown');
		//get child element
		const child = dropdown.children[0];
		child.classList.remove('hide');
		console.log('show');
	};
	const hideDropdown = () => {
		const dropdown = document.querySelector('.dropdown');
		//get child element
		const child = dropdown.children[0];
		child.classList.add('hide');
		console.log('hide');
	};
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<nav>
	<ul>
		<li>
			<a href="/">Home</a>
		</li>
		<li>
			<a href="/search">Search</a>
		</li>
		<li>
			<a href="/about">About</a>
		</li>
		<li class="dropdown" on:mouseenter={showDropdown} on:mouseleave={hideDropdown}>
			User
			<ul class="hide vert">
				<li>
					<a href="/auth/login">Login</a>
				</li>
				<li>
					<a href="/auth/register">Register</a>
				</li>
			</ul>
		</li>
	</ul>
</nav>
<slot />

<style>
	nav ul {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
	}
	nav ul li {
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		margin: 0.5rem;
	}

	.vert {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	a {
		text-decoration: none;
		color: #000;
		font-size: 1.2rem;
		font-weight: bold;
		text-transform: uppercase;
	}

	.dropdown {
		text-decoration: none;
		color: #000;
		font-size: 1.2rem;
		font-weight: bold;
		text-transform: uppercase;
		outline: none;
	}

	.dropdown:hover {
		color: #f00;
		cursor: pointer;
	}

	a:hover {
		color: #f00;
	}

	.hide {
		display: none;
	}
</style>
