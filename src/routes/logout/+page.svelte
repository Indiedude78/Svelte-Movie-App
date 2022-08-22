<script>
    import { browser } from "$app/env";
    if (browser) {
        localStorage.removeItem("user");
        window.location.href = "/auth/login";
    }
</script>

<h1>Logging Out...</h1>
