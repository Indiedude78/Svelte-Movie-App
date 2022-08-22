<script>
    import AppCss from "./../app.css";
    import { browser } from "$app/env";
    let user;
    if (browser) {
        user = localStorage.getItem("user");
    }
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
        {#if user != null}
            <li>
                <a href="/">Home</a>
            </li>
            <li>
                <a href="/search">Search</a>
            </li>
            <li>
                <a href="/about">About</a>
            </li>
            <li>
                <a href="/logout">Logout</a>
            </li>
        {:else}
            <li>
                <a href="/auth/login">Login</a>
            </li>
            <li>
                <a href="/auth/register">Register</a>
            </li>
        {/if}
    </ul>
</nav>

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

    a {
        text-decoration: none;
        color: #000;
        font-size: 1.2rem;
        font-weight: bold;
        text-transform: uppercase;
    }

    a:hover {
        color: #f00;
    }
</style>
