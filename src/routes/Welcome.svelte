<script>
  import { onMount } from 'svelte';

  let DotLottiePlayer;

  onMount(async () => {
    if (typeof window !== 'undefined') {
      const module = await import('@dotlottie/player-component');
      DotLottiePlayer = module.default;
    }
  });

  let showEnded = false;
  let playerVisible = true;
  function handleAnimationComplete() {
    playerVisible = false;
    showEnded = true;
  }
</script>

{#if playerVisible}
  <div class="player-container">
    <dotlottie-player 
        on:complete={handleAnimationComplete}
        src="https://lottie.host/fd36e9cc-2cd6-4956-8751-2549d5abe64f/PsTImqB3O2.json"
        background="transparent" 
        speed="1" 
        style="width: 57rem; height: 32rem;" 
        autoplay>
    </dotlottie-player>
  </div>
{/if}

{#if showEnded}
  <div class="greeting">
    <h1>Hi there!</h1>
  </div>
{/if}

<style>
  .player-container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>

<!-- TODO: fix window fullscreen content scaling, add something after this animation, fix draggable bug-->