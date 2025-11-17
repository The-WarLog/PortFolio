<template>
  <div id="github" class="window github" role="dialog" aria-label="Gtihub window" :draggable="true"
    :style="{ left: position.x + 'px', top: position.y + 'px' }">
    <div class="title-bar" @mousedown="startDrag">
      <slot></slot>
      <div class="title-bar-text">Github</div>
      <div class="title-bar-controls" aria-hidden="false">
        <button aria-label="Minimize" class="btn-min" @click="emit('minimize')"></button>
        <button aria-label="Close" class="btn-close" @click="emit('close')"></button>
      </div>
    </div>

    <div class="window-body">
      <h5>Welcome to my Gtihub you can access it via</h5> <span> <a class="link text-lg" target="_blank"
          href="https://github.com/The-WarLog"> https://github.com/The-WarLog</a></span>


    </div>
    <div class="inside-buttons">
      <button class="default" @click="redirectToGithub">OK</button>
      <button class="default" @click="emit('close')">Cancel</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, ref, onUnmounted } from 'vue';
// const props = defineProps<{
//   open?: boolean
// }>()
const emit = defineEmits(['close', 'minimize']);
//tracking position
const position = ref({ x: 100, y: 100 });
//dragging state
const isDragging = ref(false);
const dragOffset = ref({ x: 0, y: 0 })

function startDrag(event: MouseEvent) {
  if ((event.target as HTMLElement).tagName === "BUTTON") return; //prevent dragging when clicking buttons
  isDragging.value = true;
  dragOffset.value = {
    x: event.clientX - position.value.x,
    y: event.clientY - position.value.y
  }
  document.addEventListener('mousemove', onDrag);
  document.addEventListener('mouseup', stopDrag);
  event.preventDefault()
}
function onDrag(event: MouseEvent) {
  if (isDragging.value === false) return;
  //updating the postion
  position.value = {
    x: event.clientX - dragOffset.value.x,
    y: event.clientY - dragOffset.value.y
  }

  //YEEEEE
}
function stopDrag() {
  isDragging.value = false
  //remoing the event listeners
  document.removeEventListener('mousemove', onDrag);
  document.removeEventListener('mouseup', stopDrag)
}  //cleanup on unmount
onUnmounted(() => {
  document.removeEventListener('mousemove', onDrag);
  document.removeEventListener('mouseup', stopDrag)
})
function redirectToGithub() {
  window.open('https://github.com/The-WarLog', '_blank');
}


</script>

<style>
.github .inside-buttons {
  display: flex;
  justify-content: flex-end;
  padding: 8px;
  gap: 8px;
}

/* container size similar to your screenshot */
.github {
  width: 500px;
  height: 170px;
  box-sizing: border-box;
  padding: 3px;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #dfdfdf,
    inset -2px -2px grey, inset 2px 2px #fff;
  background: silver;
  display: flex;
  flex-direction: column;
  position: fixed;
  user-select: none;
}

/* Title bar styling (blue gradient like Windows 98) */
.title-bar {
  background: linear-gradient(90deg, #0b2c73 0%, #1a7ad3 60%);
  padding: 4px 6px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 30px;
  box-sizing: border-box;


}

/* Title text */
.title-bar-text {
  color: #ffffff;
  font-weight: 700;
  font-size: 14px;
  text-shadow: 0 1px rgba(0, 0, 0, 0.35);
  padding-left: 6px;
}

/* Controls container */
.title-bar-controls {
  display: flex;
  gap: 6px;
  align-items: center;
}

/* Base button visual (small square) */
.title-bar-controls button {
  display: inline-block;
  width: 16px;
  height: 14px;
  padding: 0;
  margin: 0;
  border: none;
  background: silver;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #fff,
    inset -2px -2px grey, inset 2px 2px #dfdfdf;
  outline: none;
  cursor: pointer;
}

/* Minimize icon (tiny black bar) */
.btn-min {
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='8' height='3'><rect width='8' height='2' y='1' fill='%23000'/></svg>");
  background-repeat: no-repeat;
  background-position: center;
  background-color: silver;
}

/* Close icon (classic X) */
.btn-close {
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='8' height='8'><path d='M1 1 L7 7 M7 1 L1 7' stroke='%23000' stroke-width='1.2' stroke-linecap='square' /></svg>");
  background-repeat: no-repeat;
  background-position: center;
}

/* button press effect */
.title-bar-controls button:active {
  transform: translateY(1px);
  box-shadow: inset -1px -1px #fff, inset 1px 1px #0a0a0a,
    inset -2px -2px #dfdfdf, inset 2px 2px grey;
}

/* window body layout */
.window-body {
  margin: 8px;
  padding: 20px 16px;
  flex: 1 1 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #c0c0c0;
}

.default {
  min-width: 75px;
  min-height: 23px;
  padding: 3px 12px;
  font-family: "MS Sans Serif", "Segoe UI", Tahoma, sans-serif;
  font-size: 11px;
  color: #000000;
  background: silver;
  border: none;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #ffffff,
    inset -2px -2px grey, inset 2px 2px #dfdfdf;
  cursor: pointer;
  outline: none;
}

/* Button hover effect */
.default:hover {
  background: #d8d8d8;
}

/* Button active/pressed effect */
.default:active {
  box-shadow: inset -1px -1px #ffffff, inset 1px 1px #0a0a0a,
    inset -2px -2px #dfdfdf, inset 2px 2px grey;
  padding: 4px 11px 2px 13px;
}








/* small responsive tweak: full width on small screens */
@media (max-width: 600px) {
  .about-me {
    width: 95%;
    max-width: 95%;
    height: 500px;
  }

  #about-text {
    font-size: 18px;
  }
}
</style>
