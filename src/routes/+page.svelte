<script>
	import { browser } from "$app/env";
	let user;
	if (browser) {
		user = localStorage.getItem("user");
		if (user) {
			window.location.href = "/home";
		}
	}
</script>

<h1>Welcome to the movie sharing app</h1>
