<script>
  import MovieItem from "./Movie/Item.svelte";
  import { onMount } from "svelte";

  const APIKEY = "4d34fed296059cb1dd1ba88983ebbd3e";
  const BASEURL = `https://api.themoviedb.org/3`;
  const APISETTINGS = `?api_key=${APIKEY}&language=es-MX`;
  let movies = [];

  function fetchMovies() {
    const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`;

    fetch(URL)
      .then(res => res.json())
      .then(({ results }) => {
        movies = results;
        console.log(results);
      });
  }

  onMount(() => {
    console.log("the component has mounted");
    fetchMovies();
  });
</script>

<style>
  @media (min-width: 640px) {
    main {
      max-width: 100vh;
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
    {#each movies as movie}
      <div class="col-12 col-md-6 col-lg-3 p-2">
        <MovieItem
          id={movie.id}
          title={movie.title}
          overview={movie.overview}
          release_date={movie.release_date}
          cover={movie.poster_path} />
      </div>
    {/each}

  </div>

</main>
