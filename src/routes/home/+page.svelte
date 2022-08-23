<script>
    import { browser } from "$app/env";
    import Card from "../../components/mediacard.svelte";
    let jwt;
    let token;
    let authorized_user;
    let fname, lname, id, email, username;

    const count = Array(10).fill(0);
    if (browser) {
        jwt = localStorage.getItem("user");
        token = jwt;
        if (!token) {
            window.location.href = "/";
        }
    }

    //fetch user from api
    async function getUser() {
        const res = await fetch(
            "http://192.168.1.142/movie-api/protected/profile.php",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    token,
                }),
            }
        );
        const data = await res.json();
        if (data) {
            authorized_user = data.data;
            if (authorized_user) {
                fname = authorized_user.firstname;
                lname = authorized_user.lastname;
                id = authorized_user.id;
                email = authorized_user.email;
                username = authorized_user.username;
                console.log(authorized_user);
            }
        } else {
            console.log("false");
        }
    }
    getUser();
</script>

<h1>
    Welcome
    {#if fname}
        {fname}
    {/if}
</h1>
<svelte:head>
    <title>Watch with me</title>
</svelte:head>
<div class="movie-list">
    {#each count as i}
        <Card />
    {/each}
</div>

<style>
    .movie-list {
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        flex-wrap: wrap;
    }
</style>
