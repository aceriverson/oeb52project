<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';
  
    import fern from './assets/ferns/fern.png';
    import next from './assets/next.svg';
    import sun from './assets/sun.png';
    import { state } from './stores';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "A new taxa in the land plants has emerged!";
    } else if (chapterState == 1) {
        displayText = "The seedless vascular plants of ferns and lycophytes.";
    } else if (chapterState == 2) {
        displayText = "The evolution of true roots allows these plants to find more nutrients.";
        isNextVisible = false;
    } else if (chapterState == 5) {
        displayText = "Additionally, these plants evolved complex vascular systems to transport water and nutrients.";
        isNextVisible = true;
    } else if (chapterState == 6) {
        displayText = "Vascular tissue allows these plants to grow even taller too!";
    } else if (chapterState == 7) {
        displayText = "";
        isNextVisible = false;
    } else if (chapterState == 9) {
        displayText = "Oh no, the ability to grow taller means some plants are blocking out your light!";
        isNextVisible = true;
    } else if (chapterState == 10) {
        displayText = "This sounds like another adaptation would be advantageous to compete.";
    } else if (chapterState == 11) {
        state.set("aboveferns");
    }
    
</script>
    
<main in:fade="{{delay: 1000}}" out:fade>
    {#if chapterState < 6}
    <img transition:fade class="plant1 animate__animated animate__slower animate__pulse animate__infinite" src={fern} />
    {:else}
    <img transition:fade="{{delay: 1000}}" class="plant2 animate__animated animate__slower animate__pulse animate__infinite" src={fern} />
    {/if}

    {#if chapterState >= 2}
    <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut1 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>N2</h2>
    <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut2 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>CO2</h2>
    <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut3 animate__animated animate__slower animate__flip animate__infinite" on:click={(e) => {e.target.remove(); chapterState++}}>P</h2>
    {/if}

    {#if chapterState >= 7}
    <img transition:fly="{{ y: 200, duration: 2000 }}" class="sun1 animate__animated" src={sun} on:click={(e) => {e.target.classList.toggle("animate__headShake"); chapterState < 9 ? chapterState++ : null}} />
    <img transition:fly="{{ y: 200, duration: 2000 }}" class="sun2 animate__animated" src={sun} on:click={(e) => {e.target.classList.toggle("animate__headShake"); chapterState < 9 ? chapterState++ : null}} />
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
        background: url('./assets/ferns.jpg') no-repeat center center fixed; 
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
    }
  
    .plant1 {
        width: 20rem;
        margin: 25% auto;
    }

    .plant2 {
        width: 20rem;
        height: 30rem;
        margin: 15% 25% 25% 25%;
    }

    .sun1 {
        position: absolute;
        top: 5%;
        right: 35%;
        width: 3rem;
    }

    .sun2 {
        position: absolute;
        top: 10%;
        left: 35%;
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


    .nut1 {
        position: absolute;
        bottom: 30%;
        left: 34%;
        color: chocolate;
    }

    .nut2 {
        position: absolute;
        bottom: 25%;
        right: calc(50% - 1.5rem);
        color: #ff3e00;
    }

    .nut3 {
        position: absolute;
        bottom: 30%;
        right: 34%;
        color: aqua
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
  