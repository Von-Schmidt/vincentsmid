<script>
    import { windows } from './store.js';
    import { onMount } from 'svelte';
    let id = 0;
  
    function openApp(title, body) {
      windows.update(n => [...n, { id: id++, content: { title, body } }]);
    }

    onMount(() => {
      openApp('Road ahead', 'Welcome to a half-baked website. This is a work in progress.');
    });
</script>
  
  <div class="taskbar-container">
    <div class="taskbar">
      <button on:click={() => openApp('test', 'test-body')}>1</button>
      <button on:click={() => openApp('test', 'test-body')}>2</button>
      <button on:click={() => openApp('test', 'test-body')}>3</button>
      <button on:click={() => openApp('test', 'test-body')}>4</button>
      <button on:click={() => openApp('test', 'test-body')}>5</button>
      <button on:click={() => openApp('test', 'test-body')}>6</button>
      <button on:click={() => openApp('test', 'test-body')}>7</button>
      <button on:click={() => openApp('test', 'test-body')}>8</button>
      <button on:click={() => openApp('test', 'test-body')}>9</button>
      <button on:click={() => openApp('test', 'test-body')}>10</button>
    </div>
  </div>
  
  <style>
    .taskbar {
      display: flex;
      justify-content: space-evenly;
      align-items: center;
      color: white;
      border-radius: 0.8rem;
      background: rgba(146, 241, 241, 0.4);
      box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
      backdrop-filter: blur(0.2rem);
      width: 58.6rem;
      height: 6.9rem;
    }
  
    .taskbar-container {
      position: fixed;
      left: 50%;
      bottom: 1rem;
      transform: translateX(-50%);
      z-index: 1000;
    }
  
    button {
      width: 4.7rem;
      height: 4.8rem;
      border-radius: 0.8rem;
      border: none;
      background: white;
      opacity: 1;
      box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
    }

    button:hover {
      opacity: 0.8;
      cursor: grab;
    }
  </style>
  
  