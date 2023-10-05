<script>
    import { windows } from './store.js';
    import { onMount } from 'svelte';
    let id = 0;
  
    function openApp(title, body) {
      windows.update(n => [...n, { id: id++, content: { title, body } }]);
    }

    onMount(() => {
      openApp('About me', 'I Stink')
    });
</script>
  
  <div class="taskbar-container">
    <div class="taskbar">
      <button on:click={() => openApp('About me', 'THIS PAGE IS UNDERGOING DEVELOPMENT')}>About me</button>
      <button on:click={() => openApp('LOL', 'asdf')}>App 2</button>
    </div>
  </div>
  
  <style>
    .taskbar {
      display: flex;
      justify-content: center;
      align-items: center;
      color: white;
      border-radius: 0.8rem;
      background: rgba(146, 241, 241, 0.4);
      box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
      backdrop-filter: blur(0.2rem);
      width: 47.9rem; /* Based on 479px original */
      height: 5.6rem; /* Based on 56px original */
    }
  
    .taskbar-container {
      position: fixed;
      left: 50%;
      bottom: 1rem; /* 10px based on your design */
      transform: translateX(-50%);
      z-index: 1000;
    }
  
    button {
      width: 3.8rem; /* Based on 38px original */
      height: 3.8rem; /* Based on 38px original */
      border-radius: 0.8rem;
      border: none;
      background: white;
      opacity: 1; /* to override the taskbar's opacity */
      box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
    }
  </style>
  
  