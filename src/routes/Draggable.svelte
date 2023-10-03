<script>
  let isDragging = false;

  function onMouseDown(event) {
    isDragging = true;

    let draggedElem = event.currentTarget.parentElement.parentElement;
    let startX = parseInt(draggedElem.style.left || 0) - event.clientX;
    let startY = parseInt(draggedElem.style.top || 0) - event.clientY;

    function onMouseMove(event) {
      if (isDragging) {
        draggedElem.style.left = `${event.clientX + startX}px`;
        draggedElem.style.top = `${event.clientY + startY}px`;
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

<div on:mousedown={onMouseDown}>
  <slot></slot>
</div>
