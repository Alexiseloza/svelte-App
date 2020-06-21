<script>
  export let id;
  export let title;
  export let release_date;
  export let overview;
  export let cover;

  $: coverURL = `https://image.tmdb.org/t/p/w185_and_h278_bestv2${cover}`;
</script>

<div class="card">
  <img src={coverURL} class="card-img-top" alt="..." />
  <div class="card-body">
    <h5 class="card-title">{title}</h5>
    <p class="card-text">{overview}</p>
    <p class="card-text">Start Date.{release_date}</p>
    <div class="text-center">
      <button class="btn btn-primary">Like</button>
    </div>
  </div>
</div>
