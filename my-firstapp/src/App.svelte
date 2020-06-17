<script>
  export let name;
  let points = 50;
  const showControls = true;

  const addPoint = () => (points += 1);
  const removePoint = () => (points -= 1);
  const toggleControls = () => (showControls = !showControls);
</script>

<style>
  h1 {
    color: blue;
  }

  @media (min-width: 640px) {
    main {
      max-width: 100vh;
    }
  }
</style>

<main class="container">
  <div class="card">
    <h1>
      {name}
      <button class="btn btn-sm" on:click={toggleControls}>
        {#if showControls}-{:else}+{/if}
      </button>
    </h1>
    <h3 class="text-center mb-5">Your Points: {points}!</h3>
    {#if showControls}
      <button class="btn btn-success" on:click={addPoint}>+1</button>
      <button class="btn btn-warning" on:click={removePoint}>-1</button>

      <input class="my-3" type="number" bind:value={points} />
    {/if}

  </div>

</main>
