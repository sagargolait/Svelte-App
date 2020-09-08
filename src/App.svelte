<script>
  let search = "";
  let loading = false;
  let gifs = [];
  const API_URL =
    "https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=";

  async function SearchGif(e) {
    e.preventDefault();
    loading = true;
    gifs = [];
    const response = await fetch(`${API_URL}${search}`);
    const json = await response.json();
    gifs = json.data.map((gif) => gif.images.fixed_height.url);
    loading = false;
  }
</script>

<style>
  main {
    text-align: center;
  }
</style>

<main>
  <form on:submit={SearchGif}>
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label>Search GIF</label>
    <input
      type="text"
      bind:value={search}
      id="search"
      name="search"
      placeholder="Search Gifphy" />
    <button type="submit">GO!</button>
  </form>
  {#if loading}
    <img
      src={'https://media2.giphy.com/media/l3nWhI38IWDofyDrW/giphy.gif?cid=790b76115d055ab7424f75514dcb4d7a&rid=giphy.gif'}
      alt="loading" />
  {/if}

  {#each gifs as gif}<img src={gif} alt="gif" />{/each}
</main>
