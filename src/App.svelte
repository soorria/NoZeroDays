<script>
  import { onMount } from "svelte";
  const today = new Date();
  const todayString = `${today.getDate()}-${today.getMonth()}-${today.getFullYear()}`;
  const localStorageKey = "nzd:days";
  let days = JSON.parse(localStorage.getItem(localStorageKey)) || {};

  $: localStorage.setItem(localStorageKey, JSON.stringify(days));

  function handleYes() {
    days[todayString] = true;
  }

  function handleNo() {
    days[todayString] = false;
  }
</script>

<style>
  main {
    height: 100%;
    max-height: 100%;
    text-align: center;
    padding: 1em;
    max-width: none;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3.5em;
    font-weight: 300;
    margin: 0 auto;
  }

  h2 {
    text-transform: uppercase;
    font-size: 1.3rem;
  }

  .grid {
    display: grid;
    grid-template-rows: repeat(2, 1fr);
    grid-gap: 10px;
    flex-grow: 1;
  }

  .column {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
  }

  button {
    width: 100%;
    cursor: pointer;
    font-size: 3rem;
    margin: 0;
    border: none;
    transition: all 300ms;
  }
  button:hover {
    filter: brightness(0.9);
  }

  button:active {
    filter: brightness(0.8);
  }

  button:focus {
    outline: none;
  }

  button small {
    font-size: 1.5rem;
  }

  button.yes {
    background-color: lightgreen;
  }

  button.yes:focus {
    box-shadow: 0 0 0 5px rgba(144, 238, 144, 0.5);
  }

  button.no {
    background-color: lightpink;
  }

  button.no:focus {
    box-shadow: 0 0 0 5px rgba(255, 182, 193, 0.5);
  }

  @media (min-width: 640px) {
    main {
      max-width: 800px;
    }

    .grid {
      grid-template-rows: none;
      grid-template-columns: repeat(2, 1fr);
      height: 500px;
      flex-grow: 0;
    }

    .column {
      justify-content: center;
    }
  }
</style>

<main class="column">
  <h1>No Zero Days!</h1>

  {#if days[todayString] === true}
    <h2>Today was a non-zero day!</h2>
  {:else if days[todayString] === false}
    <h2>Today isn't a non-zero day yet. You still have time!</h2>
  {:else}
    <h2>Was today a non-zero day?</h2>
  {/if}

  <div class="grid">
    <button class="yes" on:click={handleYes}>
      Yes
      <br />
      <small>I did things today!</small>
    </button>
    <button class="no" on:click={handleNo}>
      No
      <br />
      <small>I need to do things.</small>
    </button>
  </div>
</main>
