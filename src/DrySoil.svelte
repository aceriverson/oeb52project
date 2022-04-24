<script>
    import { fade, fly } from 'svelte/transition';
    import 'animate.css';
  
    import next from './assets/next.svg';
    import moss from './assets/soil/moss.png';
    import root from './assets/soil/root.png';
    import sun from './assets/sun.png';
    import { state } from './stores';
  
    let chapterState = 0;
    let isNextVisible = true
  
    let displayText = "";

    $: if (chapterState == 0) {
        displayText = "With the evolution of a stomata along with the waxy cuticle, a new taxa emerges among land plants.";
    } else if (chapterState == 1) {
        displayText = "The Bryophytes consist of mosses, liverworts, and hornworts.";
    } else if (chapterState == 2) {
        displayText = "You are a moss, with your tall sporophyte growing out of the gametophyte,";
    } else if (chapterState == 3) {
        displayText = "You are able to spread your spores without the need for large bodies of water.";
    } else if (chapterState == 4) {
        displayText = "Your waxy cuticle traps water in, and stomata in your leaves allow you to control the loss of water";
        isNextVisible = false;
    } else if (chapterState == 6) {
        isNextVisible = true;
    } else if (chapterState == 7) {
        displayText = "";
        isNextVisible = false;
    } else if (chapterState == 10) {
        displayText = "Bryophytes have short rhizomes which can anchor them in place,";
        isNextVisible = true;
    } else if (chapterState == 11) {
        displayText = "but they cannot reach deep into the ground to find more nutrients";
    } else if (chapterState == 12) {
        displayText = "You need another adaptation to survive in the increasingly competitive environment.";
    } else if (chapterState == 13) {
        state.set("ferns");
    }
    
</script>
    
<main in:fade="{{delay: 1000}}" out:fade>
    <img class="plant animate__animated animate__slower animate__pulse animate__infinite" src={moss} />

    {#if chapterState >= 4}
    <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun1 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
    <img transition:fly="{{ y: -200, duration: 2000 }}" class="sun2 animate__animated animate__slower animate__flip animate__infinite" src={sun} on:click={(e) => {e.target.remove(); chapterState++}} />
    {/if}

    {#if chapterState >= 7 && chapterState < 12}
    <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut1 animate__animated" on:click={(e) => {e.target.classList.toggle("animate__headShake"); chapterState++}}>N2</h2>
    <h2 transition:fly="{{ y: 200, duration: 2000 }}" class="nut2 animate__animated" on:click={(e) => {e.target.classList.toggle("animate__headShake"); chapterState++}}>P</h2>
    {/if}

    {#if chapterState >= 11}
    <img transition:fly="{{ x: -200, duration: 4000 }}" class="root1" src={root} />
    <img transition:fly="{{ x: 200, duration: 4000 }}" class="root2" src={root} />
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
        background: url('./assets/dry_soil.png') no-repeat center center fixed; 
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

    .nut1 {
        position: absolute;
        bottom: 20%;
        left: 24%;
        color: chocolate;
    }

    .nut2 {
        position: absolute;
        bottom: 23%;
        right: 34%;
        color: aqua
    }

    .root1 {
        position: absolute;
        bottom: 10%;
        right: -20%;
    }

    .root2 {
        transform: scaleX(-1);
        position: absolute;
        bottom: 0%;
        left: -20%;
    }

    .sun1 {
        position: absolute;
        top: 30%;
        left: 35%;
        width: 3rem;
    }

    .sun2 {
        position: absolute;
        top: 30%;
        right: 35%;
        width: 3rem;
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
  