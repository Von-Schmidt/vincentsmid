<script>
  import Draggable from './Draggable.svelte';
  import { windows } from './store.js';
  import { fly } from 'svelte/transition';

  function closeWindow(id) {
    windows.update(n => n.filter(win => win.id !== id));
  }

  let maximizedWindows = new Set();

  function toggleWindowMaximized(id) {
      let windowElem = document.querySelector(`.window[data-id="${id}"]`);
      if (maximizedWindows.has(id)) {
          maximizedWindows.delete(id);
          if (windowElem) {
              windowElem.style.top = '50%';
              windowElem.style.left = '50%';
              windowElem.style.transform = 'translate(-50%, 0%)';
          }
      } else {
          maximizedWindows.add(id);
          if (windowElem) {
              windowElem.style.top = '50%';
              windowElem.style.left = '50%';
              windowElem.style.transform = 'translate(-50%, -50%)';
          }
      }
      maximizedWindows = new Set(maximizedWindows);
  }
</script>

{#each $windows as {id, content}}
  <div in:fly="{{ y: -200, duration: 300 }}" out:fly="{{ y: 200, duration: 300 }}">
      <div class="window" class:maximized={maximizedWindows.has(id)} data-id={id}>
          {#if !maximizedWindows.has(id)}
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
                        <button class="button-close" on:click={() => toggleWindowMaximized(id)}></button>
                        <button class="button-close" on:click={() => closeWindow(id)}></button>
                      </div>
                  </div>
              </Draggable>
          {:else}
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
                      <button class="button-close" on:click={() => toggleWindowMaximized(id)}></button>
                      <button class="button-close" on:click={() => closeWindow(id)}></button>
                  </div>
              </div>
          {/if}
          <div class="window-content">
              <svelte:component this={content.body} />
          </div>
      </div>
  </div>
{/each}

<style>
  .window {
    position: relative;
    width: 60rem;
    height: 40rem;
    background-color: white;
    border-radius: 0.8rem;
    box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
  }

  .title-bar {
    background-color: #DFDFDF;
    height: 3rem;
    border-top-left-radius: 0.8rem;
    border-top-right-radius: 0.8rem;
    user-select: none;
    cursor: grab;
    color: #676767;
    text-align: center;
    font-size: 1.3rem;
    font-weight: 600;
    line-height: normal;
    justify-content: space-between;
  }

  .container {
    display: flex;
    align-items: center;
  }

  .button-box {
    width: 6.4rem;
    height: 2.2rem;
    border-radius: 0.8rem;
    background: #D4D4D4;
    box-shadow: 0 0.4rem 0.4rem rgba(0, 0, 0, 0.25);
    margin-left: 0.8rem;
    margin-right: 0.4rem;
    justify-content: space-around;
  }

  .button-close {
    display: inline-block;
    width: 1.6rem;
    height: 1.6rem;
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
    width: 2.6rem;
    margin-left: 1rem;
  }

  .window-content {
    padding: 1rem;
  }

  .window.maximized {
      width: 100vw;
      height: 100vh;
      border-radius: 0;
      box-shadow: none;
      position: fixed !important;
      top: 50%;           /* Center the window vertically */
      left: 50%;          /* Center the window horizontally */
      transform: translate(-50%, -50%); /* Correct the positioning for true center */
      z-index: 11;
  }
</style>
