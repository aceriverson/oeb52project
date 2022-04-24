<script>
  import { state } from './stores.js'

  import Ocean from './Ocean.svelte';
  import Puddle from './Puddle.svelte';
  import DrySoil from './DrySoil.svelte'
  import Ferns from './Ferns.svelte'
  import AboveFerns from './AboveFerns.svelte'
  import Forest from './Forest.svelte'

  // let clicks = 0;
</script>

<main>
  <form>
    <select id="chapters" name="chapters" bind:value={$state}>
      <option value="ocean">Ocean</option>
      <option value="puddle">Puddle</option>
      <option value="drysoil">Soil</option>
      <option value="ferns">Ferns</option>
      <option value="aboveferns">Above the Ferns</option>
      <option value="forest">Forest</option>
    </select>
  </form>
  {#if $state === "ocean"}
  <Ocean />
  {/if}
  {#if $state === "puddle"}
  <Puddle />
  {/if}
  {#if $state === "drysoil"}
  <DrySoil />
  {/if}
  {#if $state === "ferns"}
  <Ferns />
  {/if}
  {#if $state === "aboveferns"}
  <AboveFerns />
  {/if}
  {#if $state === "forest"}
  <Forest />
  {/if}
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    /* margin: 0 auto; */
    height: 100%;
    /* background: url('./assets/ocean.jpg') no-repeat center center fixed;  */
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  form {
    position: fixed;
    right: 5px;
    top: 5px;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
