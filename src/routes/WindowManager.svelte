<script>
    import Draggable from './Draggable.svelte';
    import { windows } from './store.js';
  
    function closeWindow(id) {
      windows.update(n => n.filter(win => win.id !== id));
    }
</script>
  
  {#each $windows as {id, content}}
    <div class="irix-border">
      <div class="irix-inner">
        <Draggable>
          <div class="title-bar">
            <button on:click={() => closeWindow(id)}>X</button>
            <span>{content.title}</span>
          </div>
        </Draggable>
        <div class="window-content">
          {content.body}
        </div>
      </div>
    </div>
  {/each}
  
<style>
  .title-bar {
    position: relative;
    background-color: var(--color-theme-3);
    padding: 4px;
    font-size: 14px;
    font-weight: bold;
    font-style: italic;
    color: white;
    z-index: 2;
    cursor: grab;
    border-bottom: 1px solid darkslategray;
  }

  .title-bar:before {
    border-bottom: 2px solid black;
  }

  .title-bar:after {
    border-bottom: 1px solid #999;
    
  }

  .title-bar:before, .title-bar:after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
  }

  .window-content {
    padding: 10px;
    border-top: 1px solid black;
    z-index: 2;
  }


  .irix-border {
    position: relative;
    width: 300px;
    height: 200px;
    background-color: var(--color-theme-4); /* Adjust as per your needs */
    border: 1px solid black; /* Base border color */
  }
  
  .irix-border:before, .irix-border:after, .irix-inner:before, .irix-inner:after {
    content: "";
    position: absolute;
    box-sizing: border-box;
  }
  
  /* Outer top and left light border */
  .irix-border:before {
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border-top: 1px solid #999;
    border-left: 1px solid #999;
    z-index: 1;
  }
  
  /* Inner bottom and right dark border */
  .irix-inner:after {
    right: 0px;
    bottom: 0px;
    left: 0px;
    top: 0px;
    border-right: 1px solid black;
    border-bottom: 1px solid black;
    z-index: 1;
  }
  
  /* Outer bottom and right slightly-lighter border */
  .irix-border:after {
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border-right: 1px solid #999;
    border-bottom: 1px solid #999;
    z-index: 1;
  }
  
  /* Inner top and left slightly-darker border */
  .irix-inner:before {
    right: 0px;
    bottom: 0px;
    left: 0px;
    top: 0px;
    border-left: 1px solid black;
    border-top: 1px solid black;
    z-index: 1;
  }
  
  .irix-inner {
    position: absolute;
    top: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px;
    border: 2px solid darkslategray;
  }
</style>
