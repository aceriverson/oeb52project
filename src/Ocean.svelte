<script>
// @ts-nocheck

  import { fade, fly } from 'svelte/transition';
  import 'animate.css';

  import { state } from './stores.js'

  import next from './assets/next.svg';
  import sun from './assets/sun.png';
  import spirogyra from './assets/ocean/spirogyra.png';

  let chapterState = 0;
  let isNextVisible = true

  let displayText = "You are a spirogyra, filamentous green algae floating in the water.";

  $: if (chapterState == 1) {
      displayText = "You capture light that peeks through the water's surface.";
      isNextVisible = false;
  } else if (chapterState == 4) {
      isNextVisible = true;
  } else if (chapterState == 5) {
      displayText = "You uptake nutrients dissolved in the water.";
      isNextVisible = false;
  } else if (chapterState == 8) {
      displayText =  "Life is great, right?";
      isNextVisible = true;
  } else if (chapterState == 9) {
      state.set("puddle");
  }
</script>
  
<main in:fade="{{delay: 1000}}" out:fade>
  <img class="plant animate__animated animate__slower animate__pulse animate__infinite" src={spirogyra} />
  <div class="card">
    <h1 class="animate__animated animate__slideInLeft">{displayText}</h1>
    {#if isNextVisible}
    <img class="next" src={next} on:click={() => chapterState++} />
    {/if}
  </div>
  {#if chapterState >= 1}
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun1 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun2 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun3 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  {/if}
  {#if chapterState >=  5}
  <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut1 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>N2</h2>
  <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut2 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>CO2</h2>
  <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut3 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>P</h2>
  {/if}
</main>
  
<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    height: 100%;
    background: url('./assets/Ocean.jpg') no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }

  .plant {
    width: 16rem;
    margin: 25% auto;
  }

  .next {
    width: 2rem;
    margin-right: 1em;
  }

  .card {
    position: absolute;
    bottom: 0;
    width: 100%;
    background: cornsilk;
    display: flex;
    flex-direction: row;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 2rem;
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

  .sun1 {
    position: absolute;
    top: 30%;
    right: 24%;
    width: 3rem;
  }

  .sun2 {
    position: absolute;
    top: 25%;
    right: calc(50% - 1.5rem);
    width: 3rem;
  }

  .sun3 {
    position: absolute;
    top: 30%;
    left: 24%;
    width: 3rem;
  }

  .nut1 {
    position: absolute;
    bottom: 50%;
    left: 24%;
    color: chocolate;
  }

  .nut2 {
    position: absolute;
    bottom: 40%;
    right: calc(50% - 1.5rem);
    color: #ff3e00;
  }

  .nut3 {
    position: absolute;
    bottom: 50%;
    right: 24%;
    color: aqua
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
  