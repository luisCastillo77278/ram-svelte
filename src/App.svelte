<script>
  import Character from './lib/Character.svelte'

  let characteres = []
  let page = 1

  async function loadCharacters(){
    const resp = await fetch(
      `https://rickandmortyapi.com/api/character?page=${page}`
    )

    const data = await resp.json()
    characteres = data.results
  }

  loadCharacters()

  function nextPage(){
    page++
    loadCharacters()
  }

  function prevPage(){
    page--
    loadCharacters()
  }
</script>

<main class="container">
  <h1 class="title">Rick and Morty Svelte</h1>
  <div class="btns">
    <button class="btn" disabled={page === 1} on:click={prevPage}>Previus</button>
    <button class="btn" on:click={nextPage}>Next</button>
  </div>
  <div class="grid">
    {#each characteres as character}
      <Character character={character} />
    {/each}
  </div>
</main>