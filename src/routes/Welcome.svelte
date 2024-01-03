<script>
  import { onMount } from 'svelte';

  let DotLottiePlayer;

  onMount(async () => {
    if (typeof window !== 'undefined') {
      const module = await import('@dotlottie/player-component');
      DotLottiePlayer = module.default;
    }
  });
</script>


<dotlottie-player 
    src="https://lottie.host/fd36e9cc-2cd6-4956-8751-2549d5abe64f/PsTImqB3O2.json" 
    background="transparent" 
    speed="1" 
    style="width: 573px; height: 300px;" 
    loop 
    autoplay>
</dotlottie-player>

<!-- TODO: fix window fullscreen content scaling, add something after this animation, fix draggable bug-->