<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';

    import { state } from './stores.js';
  
    import next from './assets/next.svg';
    import ginkgo from './assets/ginkgo.png';
    import pollen from './assets/pollen.png';
    import wind from './assets/wind.png';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "By using lignin to reinforce vascular tissues, some plants are able to grow incredibly tall";
    } else if (chapterState == 1) {
        displayText = ""
    } else if (chapterState == 2) {
        displayText = "Up above the floor, there are greater winds. Could they be useful?";
    } else if (chapterState == 3) {
        isNextVisible = false;
    }
    
</script>
    
<main in:fade="{{delay: 1000}}" out:fade>
    <img class="plant animate__animated animate__slower animate__pulse animate__infinite" src={ginkgo} />

    {#if chapterState >= 1}
    <img transition:fly="{{ x: -200, duration: 1500 }}" class="wind1 animate__animated animate__slower animate__shakeX animate__infinite" src={wind} />
    <img transition:fly="{{ x: -200, duration: 1500 }}" class="wind2 animate__animated animate__slower animate__shakeX animate__infinite" src={wind} />
    {/if}

    {#if chapterState >= 3}
    <img transition:fly="{{ x: -2000, duration: 2000 }}" class="pollen1 animate__animated animate__slow animate__rubberBand animate__infinite" src={pollen} on:click={() => state.set("forest")} />
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
        background: url('./assets/above_ferns.jpg') no-repeat center center fixed; 
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
    }
  
    .plant {
        width: 16rem;
        margin: 5% auto;
    }

    .pollen1 {
        width: 16rem;
        margin: 25% auto;
    }
  
    .wind1 {
        width: 16rem;
        position: absolute;
        top: 20%;
        left: 20%
    }
  
    .wind2 {
        width: 16rem;
        position: absolute;
        top: 20%;
        right: 20%
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
  