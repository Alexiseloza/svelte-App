<script>
  import { createEventDispatcher } from "svelte";

  export let id;
  export let title;
  export let release_date;
  export let overview;
  export let cover;
  export let like;

  $: coverURL = `https://image.tmdb.org/t/p/w185_and_h278_bestv2${cover}`;

  const dispatch = createEventDispatcher();

  const toogleLike = () => {
    dispatch("onToogleLike", {
      id,
      title,
      overview,
      release_date,
      cover,
      like,
    });
  };
</script>

<div class="card">
  <img src={coverURL} class="card-img-top" alt="Movie " />
  <div class="card-body">
    <h5 class="card-title">{title}</h5>
    <h6 class="card-text">ID:{id}</h6>
    <p class="card-text">
      <span class="font-weight-bold">Description Movie:</span>
      {overview}
    </p>
    <p class="card-text">Start Date.{release_date}</p>
    <div class="text-center">
      <button
        class={like ? 'btn btn-secondary' : 'btn btn-primary'}
        on:click={toogleLike}>
        {like ? 'Unlike' : 'Like'}
      </button>
    </div>
  </div>
</div>
