<script>
// @ts-nocheck

  import { fade, fly } from 'svelte/transition';
  import 'animate.css';

  import { state } from './stores.js';

  import next from './assets/next.svg';
  import sun from './assets/sun.png';
  import spirogyra from './assets/ocean/spirogyra.png';
  import stomata from './assets/puddle/stomata.png';

  let chapterState = 0;
  let isNextVisible = true;

  let displayText = "";

  $: if (chapterState == 0) {
      displayText = "You've found yourself in a small, shallow puddle. This is nice.";
  } else if (chapterState == 1) {
      displayText = "If you can reach out above the surface of the water, CO2 is exchanged much faster as a gas.";
  } else if (chapterState == 2) {
      displayText = "";
      isNextVisible = false;
  } else if (chapterState == 8) {
      displayText = "The transition to land has a major barrier. Water is lost when CO2 is absorbed.";
      isNextVisible = true;
  } else if (chapterState == 9) {
      displayText = "Without any new adaptions, the spirogyra will dry out on land!";
  } else if (chapterState == 10) {
      displayText = "How can this be overcome?";
  } else if (chapterState == 11) {
      displayText = "";
      isNextVisible = false;
  }
</script>
  
<main in:fade="{{delay: 1000}}" out:fade>
  {#if chapterState < 2}
  <img in:fade out:fade class="plant1 animate__animated animate__slower animate__pulse animate__infinite" src={spirogyra} />
  {/if}

  {#if chapterState >= 2}
  <img in:fade out:fade style:transform={`scale(${Math.max(1 - (chapterState * 0.1), 0.2)})`} class="plant2" src={spirogyra} />
  {/if}

  {#if chapterState >= 2}
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun1 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun2 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun3 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun4 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun5 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun6 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
  {/if} 

  {#if chapterState == 11}
  <img transition:fly="{{ x: -2000, duration: 2000 }}" class="stomata1 animate__animated animate__slow animate__rubberBand animate__infinite" src={stomata} on:click={() => state.set("drysoil")} />
  {/if}

  <div class="card">
      <h1 class="animate__animated animate__slideInLeft">{displayText}</h1>
      {#if isNextVisible}
      <img class="next" src={next} on:click={() => chapterState++} />
      {/if}
  </div>
</main>
  
<style>
  :root {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
          Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
      text-align: center;
      height: 100%;
      background: url('./assets/puddle.jpg') no-repeat center center fixed; 
      -webkit-background-size: cover;
      -moz-background-size: cover;
      -o-background-size: cover;
      background-size: cover;
  }

  .plant1 {
      width: 16rem;
      margin: 25% auto;
  }

  .plant2 {
      width: 16rem;
      position: fixed;
      left: 5%;
      top: 10%;
  }

  .stomata1 {
      width: 16rem;
      margin: 25% auto;
  }

  .sun1 {
    position: absolute;
    top: 2%;
    left: 4%;
    width: 3rem;
  }

  .sun2 {
    position: absolute;
    top: 2%;
    left: 15%;
    width: 3rem;
  }

  .sun3 {
    position: absolute;
    top: 2%;
    left: 26%;
    width: 3rem;
  }

  .sun4 {
    position: absolute;
    top: 20%;
    left: 4%;
    width: 3rem;
  }

  .sun5 {
    position: absolute;
    top: 20%;
    left: 15%;
    width: 3rem;
  }

  .sun6 {
    position: absolute;
    top: 20%;
    left: 26%;
    width: 3rem;
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

  @media (min-width: 480px) {
      h1 {
          max-width: none;
      }
  
      p {
          max-width: none;
      }
  }
</style>
