<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';
  
    import next from './assets/next.svg';
    import spirogyra from './assets/ocean/spirogyra.png';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "Hello"
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
</main>
    
<style>
    :root {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
            Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
  
    main {
        text-align: center;
        height: 100%;
        background: url('./assets/above_ferns.png') no-repeat center center fixed; 
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
  
    @media (min-width: 480px) {
        h1 {
            max-width: none;
        }
  
        p {
            max-width: none;
        }
    }
</style>
  