<template>
  <div id="about-me" class="window about-me" role="dialog" aria-label="About me window" :draggable="true"
    :style="{ left: position.x + 'px', top: position.y + 'px' }">
    <div class="title-bar" @mousedown="startDrag">
      <slot></slot>
      <div class="title-bar-text">About Me</div>
      <div class="title-bar-controls" aria-hidden="false">
        <button aria-label="Minimize" class="btn-min" @click="emit('minimize')"></button>
        <button aria-label="Close" class="btn-close" @click="emit('close')"></button>
      </div>
    </div>

    <div class="window-body">
      <div class="field-row-stacked">
        <textarea id="about-text" readonly>Hey there! I'm Divyesh Gaygol, a passionate software developer with a knack for creating efficient and innovative solutions.
With a background in computer science, I specialize in full-stack development with a primary focus on Backend Development.

I know JavaScript, TypeScript, Python, Java, C/C++ and Kotlin.
I work with Node.js, Express/NestJs, Spring Boot, FastAPI and Vue.js.

Sometimes I do mobile with Kotlin and Jetpack Compose (I have a Gym App called HealthMetricPlus).

I love tackling complex problems and turning ideas into reality through code.
When I'm not coding, you can find me exploring new tech, contributing to open-source, or reading about software architecture.
Let's build something amazing together!</textarea>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, ref, onUnmounted } from 'vue';
const emit = defineEmits()
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


</script>

<style>
/* container size similar to your screenshot */
.about-me {
  width: 320px;
  max-width: 320px;
  height: 560px;
  box-sizing: border-box;
  margin: 18px;
  padding: 3px;
  /* matches 98.css padding style */
  /* classic 3D inset border */
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #dfdfdf,
    inset -2px -2px grey, inset 2px 2px #fff;
  background: silver;
  display: flex;
  flex-direction: column;
  position: fixed;

  -webkit-user-drag: auto;
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
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* big textarea to match screenshot */
#about-text {
  width: 100%;
  height: 100%;
  min-height: 520px;
  /* keeps tall shape */
  resize: none;
  padding: 14px;
  box-sizing: border-box;
  border: 1px solid #cfcfcf;
  background: #ffffff;
  font-family: "Segoe UI", Tahoma, Arial, sans-serif;
  /* large readable font like the screenshot */
  font-size: 26px;
  line-height: 1.25;
  color: #111;
  overflow: auto;
}

/* subtle scrollbar styling (modern browsers) */
#about-text::-webkit-scrollbar {
  width: 10px;
}

#about-text::-webkit-scrollbar-track {
  background: #fff;
  border-left: 1px solid #e6e6e6;
}

#about-text::-webkit-scrollbar-thumb {
  background: #bdbdbd;
  border-radius: 2px;
  border: 2px solid #fff;
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
