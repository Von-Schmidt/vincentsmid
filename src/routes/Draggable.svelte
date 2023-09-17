<script>
  let x = 0;
  let y = 0;
  let isDragging = false;

  function onMouseDown(event) {
    isDragging = true;

    let startX = x - event.clientX;
    let startY = y - event.clientY;

    function onMouseMove(event) {
      if (isDragging) {
        x = event.clientX + startX;
        y = event.clientY + startY;
      }
    }

    function onMouseUp() {
      isDragging = false;
      window.removeEventListener('mousemove', onMouseMove);
      window.removeEventListener('mouseup', onMouseUp);
    }

    window.addEventListener('mousemove', onMouseMove);
    window.addEventListener('mouseup', onMouseUp);
  }
</script>

<svelte:head>
  <style>
    .draggable {
      position: absolute;
      cursor: grab;
      user-select: none;
    }

    .draggable:active {
      cursor: grabbing;
    }
  </style>
</svelte:head>

<div class="draggable" style="left: {x}px; top: {y}px" on:mousedown={onMouseDown}>
  <slot></slot>
</div>
