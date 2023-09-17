<script>
    import Draggable from './Draggable.svelte';
    import { windows } from './store.js';
  
    function closeWindow(id) {
      windows.update(n => n.filter(win => win.id !== id));
    }
  </script>
  
  {#each $windows as {id, content}}
    <Draggable>
      <div class="window">
        <div class="title-bar">
          <button on:click={() => closeWindow(id)}>X</button>
          <span>{content.title}</span>
        </div>
        <div class="window-content">
          {content.body}
        </div>
      </div>
    </Draggable>
  {/each}
  
  <style>
    .window {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        border: 3px solid var(--color-theme-1);
        background-color: var(--color-theme-4);
        box-shadow: 0 19px 38px rgba(0,0,0,0.30), 0 15px 12px rgba(0,0,0,0.22);
    }
    .title-bar {
      background-color: var(--color-theme-3);
      padding: 5px;
      font-size: 14px;
      font-weight: bold;
      font-style: italic;
      color: white;
      cursor: grab;
    }
    .window-content {
      padding: 10px;
    }
  </style>
  