<script>
  export let left = 100;
  export let top = 100;
  export let width = 200;
  export let height = 100;

  let resizing = false;
  let dragging = false;
  let initialResizeX = 0;
  let initialResizeY = 0;
  let initialDragX = 0;
  let initialDragY = 0;

  function onMouseDown(event) {
    if (event.target.classList.contains("resize-handle")) {
      resizing = true;
      initialResizeX = event.clientX;
      initialResizeY = event.clientY;
    } else {
      dragging = true;
      initialDragX = event.clientX - left;
      initialDragY = event.clientY - top;
    }
  }

  function onMouseMove(event) {
    if (resizing) {
      width += event.clientX - initialResizeX;
      height += event.clientY - initialResizeY;
      initialResizeX = event.clientX;
      initialResizeY = event.clientY;
    } else if (dragging) {
      left = event.clientX - initialDragX;
      top = event.clientY - initialDragY;
    }
  }

  function onMouseUp() {
    resizing = false;
    dragging = false;
  }
</script>

<style>
  .draggable {
    user-select: none;
    cursor: grab;
    border: solid 2px #3498db;
    background-color: #f1f1f1;
    position: absolute;
    border-radius: 10px;
  }

  .resize-handle {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: #3498db;
    bottom: 0;
    right: 0;
    cursor: se-resize;
  }
</style>

<section
  on:mousedown={onMouseDown}
  on:mouseup={onMouseUp}
  on:mousemove={onMouseMove}
  style="left: {left}px; top: {top}px; width: {width}px; height: {height}px;"
  class="draggable"
>
  <slot></slot>
  <div class="resize-handle"></div>
</section>
