<script>
  import Draggable from './Draggable.svelte';
  import { windows } from './store.js';
  import { fly } from 'svelte/transition';

  function closeWindow(id) {
    windows.update(n => n.filter(win => win.id !== id));
  }
</script>

{#each $windows as {id, content}}
  <div in:fly="{{ y: -200, duration: 300 }}" out:fly="{{ y: 200, duration: 300 }}">
      <div class="window">
          <Draggable>
              <div class="title-bar container">
                  <button class="svg-box container">
                    <svg xmlns="http://www.w3.org/2000/svg" width="5" height="5" viewBox="0 0 5 5" fill="none">
                      <circle cx="2.5" cy="2.5" r="2.5" fill="white"/>
                    </svg>
                    <svg xmlns="http://www.w3.org/2000/svg" width="5" height="5" viewBox="0 0 5 5" fill="none">
                      <circle cx="2.5" cy="2.5" r="2.5" fill="white"/>
                    </svg>
                    <svg xmlns="http://www.w3.org/2000/svg" width="5" height="5" viewBox="0 0 5 5" fill="none">
                      <circle cx="2.5" cy="2.5" r="2.5" fill="white"/>
                    </svg>
                  </button>
                  <span>{content.title}</span>
                  <div class="button-box container">
                    <button class="button-close" on:click={() => closeWindow(id)}></button>
                    <button class="button-close" on:click={() => closeWindow(id)}></button>
                    <button class="button-close" on:click={() => closeWindow(id)}></button>
                  </div>
              </div>
          </Draggable>
          <div class="window-content">
              {content.body}
          </div>
      </div>
  </div>
{/each}

<style>
  .window {
    position: relative;
    width: 50rem; /* 500px */
    height: 40rem; /* 400px */
    background-color: white;
    border-radius: 0.8rem;
    box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
  }
  
  .title-bar {
    background-color: #DFDFDF;
    height: 3rem; /* 30px */
    border-top-left-radius: 0.8rem;
    border-top-right-radius: 0.8rem;
    user-select: none;
    cursor: grab;
    color: #676767;
    text-align: center;
    font-size: 1.3rem; /* 13px */
    font-weight: 600;
    line-height: normal;
    justify-content: space-between;
  }

  .container {
    display: flex;
    align-items: center;
  }

  .button-box {
    width: 6.4rem; /* 64px */
    height: 2.2rem; /* 22px */
    border-radius: 0.8rem;
    background: #D4D4D4;
    box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
    margin-left: 0.8rem;
    margin-right: 0.4rem;
    justify-content: space-around;
  }

  .button-close {
    display: inline-block;
    width: 1.6rem; /* 16px */
    height: 1.6rem; /* 16px */
    background-color: white;
    border: none;
    border-radius: 0.8rem;
    box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
    margin-top: 0.1rem;
  }

  .button-close:hover {
    background-color: #ff8787;
    transition: 0.5s;
  }

  .svg-box {
    background-color: transparent;
    border: none;
    color: transparent;
    justify-content: space-between;
    width: 2.6rem; /* 26px */
    margin-left: 1rem;
  }

  .window-content {
    padding: 1rem;
  }
</style>
