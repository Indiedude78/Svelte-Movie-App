<script>
    import { browser } from "$app/env";
    import { page } from "$app/stores";
    import { onMount } from "svelte";

    let token;
    let imdb_id;

    //movie variables
    let actors;
    let awards;
    let box_office;
    let country;
    let director;
    let genre;
    let language;
    let metascore;
    let plot;
    let poster;
    let rated;
    let released;
    let runtime;
    let title;
    let writer;
    let year;
    let imdb_rating;
    let data;
    if (browser) {
        token = localStorage.getItem("user");
        if (!token) {
            window.location.href = "/";
        }
    }
    imdb_id = $page.params.slug;
    onMount(async () => {
        const res = await fetch(
            "http://98.109.173.128:50014/movie-api/protected/movie.php",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    token,
                    imdb_id,
                }),
            }
        );
        data = await res.json();
        console.log(data);
        if (data.status == "success") {
            actors = data.data.actors;
            awards = data.data.awards;
            box_office = data.data.box_office;
            country = data.data.country;
            director = data.data.director;
            genre = data.data.genre;
            language = data.data.language;
            metascore = data.data.metascore;
            plot = data.data.plot;
            poster = data.data.poster;
            rated = data.data.maturity_rating;
            released = data.data.release_year;
            runtime = data.data.runtime;
            title = data.data.title;
            writer = data.data.writer;
            imdb_rating = data.data.imdb_rating;
        }
    });
</script>

{#if !actors}
    <div>
        <h1>Loading...</h1>
    </div>
{:else}
    <div>
        <div>
            <h1>{title}</h1>
            <img src={poster} alt={title} />
        </div>
        <div>
            <h2>Plot:</h2>
            <p>{plot}</p>
        </div>
        <div>
            <h2>Actors:</h2>
            <p>{actors}</p>
        </div>
        <div>
            <h2>Awards</h2>
            <p>{awards}</p>
        </div>
        <div>
            <h2>Box Office</h2>
            <p>{box_office}</p>
        </div>
        <div>
            <h2>Country</h2>
            <p>{country}</p>
        </div>
        <div>
            <h2>Director</h2>
            <p>{director}</p>
        </div>
        <div>
            <h2>Genre</h2>
            <p>{genre}</p>
        </div>
        <div>
            <h2>Language</h2>
            <p>{language}</p>
        </div>
        <div>
            <h2>Metascore</h2>
            <p>{metascore}</p>
        </div>
        <div>
            <h2>Rated</h2>
            <p>{rated}</p>
        </div>
        <div>
            <h2>Released</h2>
            <p>{released}</p>
        </div>
        <div>
            <h2>Runtime</h2>
            <p>{runtime}</p>
        </div>
        <div>
            <h2>Writer</h2>
            <p>{writer}</p>
        </div>
        <div>
            <h2>Year</h2>
            <p>{year}</p>
        </div>
        <div>
            <h2>IMDB Rating</h2>
            <p>{imdb_rating}</p>
        </div>
    </div>
{/if}
