<script>
  import MovieItem from "./Movie/Item.svelte";
  // import { onMount } from "svelte";
  import { fly } from "svelte/transition";

  const APIKEY = "4d34fed296059cb1dd1ba88983ebbd3e";
  const BASEURL = `https://api.themoviedb.org/3`;
  const APISETTINGS = `?api_key=${APIKEY}&language=es-MX`;

  // function fetchMovies() {
  //   const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`;

  //   fetch(URL)
  //     .then(res => res.json())
  //     .then(({ results }) => {
  //       movies = results;
  //       console.log(results);
  //     });
  // }

  const movies = (async () => {
    const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`;
    const response = await fetch(URL);

    return await response.json();
  })();

  // onMount(() => {
  //   console.log("the component has mounted");
  //   fetchMovies();
  // });

  let likedMovies = [];

  const toogleLike = (event) => {
    console.log(event);
    const movie = event.detail;

    let index = likedMovies.findIndex((m) => m.id === movie.id);

    if (index >= 0) {
      likedMovies.splice(index, 1);
      console.log(likedMovies);
      likedMovies = likedMovies;
      return;
    }
    likedMovies.push(movie);
    likedMovies = likedMovies;
    console.log(likedMovies);
  };

  $: like = (id) => {
    let index = likedMovies.findIndex((m) => m.id === id);
    return index >= 0;
  };
</script>

<style>
  .panel {
    height: 100vh;
    overflow: auto;
  }
  main {
    text-align: center;
    padding: 0;
    max-width: 240px;
    margin: 0 auto;
  }
  h1 {
    color: #3431f5;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  @media (min-width: 640px) {
    main {
      max-width: 100vw;
      background-color: rgb(226, 226, 226);
    }
  }
</style>

<svelte:head>
  <title>Movies API with Svelte JS | powered Alexis</title>
  <link
    rel="stylesheet"
    href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
    integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk"
    crossorigin="anonymous" />
</svelte:head>

<main class="container">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-8 border panel">
      <h1>Popular Movies</h1>
      <!-- {#each movies as movie}
      <div class="col-12 col-md-6 col-lg-3 p-2">
        <MovieItem
          id={movie.id}
          title={movie.title}
          overview={movie.overview}
          release_date={movie.release_date}
          cover={movie.poster_path} />
      </div>
    {/each} -->
      <div class="row">
        {#await movies}
          <!-- promise is pending -->
          <p>Loading...</p>
        {:then data}
          <!-- promise was fulfilled -->
          {#each data.results as movie}
            <div class="col-12 col-md-6 col-lg-4 p-1">
              <MovieItem
                like={like(movie.id)}
                title={movie.title}
                overview={movie.overview}
                release_date={movie.release_date}
                cover={movie.poster_path}
                on:onToogleLike={toogleLike} />
            </div>
          {/each}
        {/await}
      </div>

    </div>
    <div class="col-12 col-md-6 col-lg-4 border panel">
      <h2>Favorites Movies</h2>
      <div class="row">

        {#if likedMovies.length}
          {#each likedMovies as movie, i (movie.id)}
            <div
              in:fly={{ duration: 200, y: 20 }}
              out:fly={{ duration: 800, y: -20 }}
              class="col-12 col-md-6 col-lg-4 p-2">
              <MovieItem
                like={like(movie.id)}
                title={movie.title}
                overview=""
                release_date={movie.release_date}
                cover={movie.cover}
                on:onToogleLike={toogleLike} />
            </div>
          {/each}
        {:else}
          <div class="col-12">
            <p>No Movies Favorites</p>
          </div>
        {/if}
      </div>
    </div>

  </div>
  <footer>
    Powered by
    <a href="https://alexisdev.co" target="_blank">Alexis Loza</a>
  </footer>

</main>
