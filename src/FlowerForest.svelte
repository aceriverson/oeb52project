<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';
  
    import next from './assets/next.svg';
    import appleBlossom from './assets/apple_blossom.png';
    import appleTree from './assets/apple_tree.png';
    import bee from  './assets/bee.png';
    import root from './assets/soil/root.png';
    import sun from './assets/sun.png';
    import { state } from './stores';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "Our last taxa among land plants has emerged. The angiosperms.";
    } else if (chapterState == 1) {
        displayText = "Angiosperms utilize flowers to attract pollinators to their sporangia.";
    } else if (chapterState == 2) {
        displayText = "";
        isNextVisible = false;
    } else if (chapterState == 4) {
        displayText = "Using pollinators to spread pollen is efficient.";
        isNextVisible = true;
    } else if (chapterState == 5) {
        displayText = "There is pressure to attract selective pollinators, so your pollen spreads directly to other members of the same species.";
    } else if (chapterState == 6) {
        displayText = "There is no need to waste pollen in the wind as it can be carried far, right to the pistil, by pollinators.";
    } else if (chapterState == 7) {
        state.set("fin");
    };
    
</script>
    
<main in:fade="{{delay: 1000}}" out:fade>
    {#if chapterState <= 3}
    <img transition:fade class="plant animate__animated animate__slower animate__pulse animate__infinite" src={appleBlossom} />
    {/if}

    {#if chapterState == 2}
    <img in:fly="{{x: -200, duration: 2000}}" out:fade class="bee1" src={bee} on:click={() => chapterState++} />
    {/if}

    {#if chapterState == 3}
    <img in:fly="{{x: -200, y: -200, duration: 2000}}" out:fade class="bee2" src={bee} on:click={() => chapterState++} />
    {/if}

    {#if chapterState >= 4}
    <img transition:fade="{{delay: 1000}}" class="plant animate__animated animate__slower animate__pulse animate__infinite" src={appleTree} />
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
        background: url('./assets/flower_forest.jpg') no-repeat center center fixed; 
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
    }
  
    .plant {
        width: 17rem;
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

    .bee1 {
        width: 8rem;
        position: absolute;
        left: 25%;
        top: 25%;
    }

    .bee2 {
        width: 8rem;
        position: absolute;
        left: calc(50% - 4rem);
        top: 40%;
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
  