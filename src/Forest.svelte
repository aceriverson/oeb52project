<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';
  
    import next from './assets/next.svg';
    // import apple from './assets/apple.png';
    // import appleTree from './assets/apple_tree.png';
    import bee from './assets/bee.png';
    import flower from './assets/flower.png';
    import ginkgo from './assets/ginkgo.png';
    
    import { state } from './stores';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "Using lightweight pollen carried far by the air allows this new taxa, gynosperms, to travel far and wide";
    } else if (chapterState == 1) {
        displayText = "Because pollen is the gametophyte generation, wind-dispersal applies selective pressure to further shrink the gametophyte.";
    } else if (chapterState == 2) {
        displayText = "How about the sporophyte?";
    } else if (chapterState == 3) {
        displayText = "To give the next generation a better chance, the ovule can develop into a sturdy seed, to distribute its progeny both through space, and time.";
    } else if (chapterState == 4) {
        displayText = ""
        // isNextVisible = false;
    } else if (chapterState == 5) {
        displayText = "Hmm. Dispersing my pollen in the wind is terribly inefficient.";
    } else if (chapterState == 6) {
        displayText = "I wonder if those insects could be of use to someone?";
    } else if (chapterState == 7) {
        displayText = "Flowers";
        isNextVisible = false;
    } else if (chapterState == 8) {
        state.set("flowerforest");
    };
    
</script>
    
<main in:fade="{{delay: 1000}}" out:fade>
    {#if chapterState <= 6}
    <img transition:fly="{{ x: -2000, duration: 2000 }}" class="plant animate__animated animate__slower animate__pulse animate__infinite" src={ginkgo} />
    {/if}

    {#if chapterState >= 4 && chapterState <= 6}
    <img transition:fade class="bee animate__animated animate__slower animate__pulse animate__infinite" src={bee} />
    {/if}

    {#if chapterState == 7}
    <img transition:fly="{{ x: -2000, duration: 2000, delay: 500 }}" class="fruit animate__animated animate__slower animate__pulse animate__infinite" src={flower} on:click={() => chapterState++} />
    {/if}

    <!-- {#if chapterState >= 8}
    <img transition:fade="{{delay: 500}}" class="fruit animate__animated animate__slower animate__pulse animate__infinite" src={appleTree} />
    {/if} -->
  
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
        background: url('./assets/forest.jpg') no-repeat center center fixed; 
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
    }

    .bee {
        width: 12rem;
        position: absolute;
        top: 15%;
        left: 20%;
    }

    .fruit {
        width: 16rem;
        margin: 25% auto;
        /* position: absolute; */
    }
  
    .plant {
        width: 16rem;
        margin: 5% auto;
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
  