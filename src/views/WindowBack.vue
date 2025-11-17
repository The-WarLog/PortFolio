<template>
  <div class="min-h-screen w-full relative overflow-hidden bg-teal-desktop font-sans">
    <!-- Desktop icon area: 2-column stack, spaced like simo.ng -->
    <aside class="absolute top-6 left-6" style="width: 200px;" aria-hidden="true">
      <slot></slot>
      <div class="grid grid-cols-2 gap-y-8 gap-x-8">
        <!-- Row 1 -->
        <div class="icon-item text-center" @click="openWindow('aboutwindow')">
          <img src="../assets/me.645579a6.png" alt="About" class="icon-img" />
          <div class="icon-label">About Me</div>
        </div>
        <div class="icon-item text-center" @click="openWindow('githubwindow')">
          <img src="../assets/github.cedc4bda.png" alt="Github" class="icon-img" />
          <div class="icon-label">Github</div>
        </div>

        <!-- Row 2 -->
        <div class="icon-item text-center" @click="openWindow('networkwindow')">
          <img src="../assets/blog.e5e91a40.png" alt="Blog" class="icon-img" />
          <div class="icon-label">Network</div>
        </div>
        <div class="icon-item text-center">
          <img src="../assets/contact.86a7d28f.png" alt="Contact" class="icon-img" />
          <div class="icon-label">Contact</div>
        </div>

        <!-- Row 3 -->
        <div class="icon-item text-center">
          <img src="../assets/projects.ab7e2e87.png" alt="Projects" class="icon-img" />
          <div class="icon-label">Projects</div>
        </div>

      </div>
    </aside>

    <!-- empty main area to preserve desktop look -->
    <div class="w-full h-full"></div>

    <!-- AboutMe window - shown when windowvalue is true -->
    <AboutMe v-if="windows.aboutwindow && !minimize.aboutminimize" @close="closeWindow('aboutwindow')"
      @minimize="minimizeWindow('aboutminimize')" />
    <GithubCard v-if="windows.githubwindow && !minimize.githubminimize" @close="closeWindow('githubwindow')"
      @minimize="minimizeWindow('githubminimize')" />
    <NetworkCard v-if="windows.networkwindow && !minimize.networkminimize" @close="closeWindow('networkwindow')"
      @minimize="minimizeWindow('networkminimize')" />

    <!-- Static bottom "Start" taskbar / footer (no clock) -->
    <footer class="fixed left-0 right-0 bottom-0 h-14 flex items-center px-3 gap-4"
      style="background: #c0c0c0; border-top: 2px solid #ffffff; box-shadow: inset 0 1px 0 #ffffff, 0 -1px 0 #000000;"
      aria-hidden="true">

      <button aria-label="startButton"
        class="active:shadow-[inset_-1px_-1px_#fff,inset_1px_1px_#0a0a0a,inset_-2px_-2px_#dfdfdf,inset_2px_2px_gray] active:pl-1.5 active:pt-0.5">
        <h1 id="start-button" data-astro-cid-e5zwepy2=""></h1>
      </button>
      <div class="flex space-x-2"></div>
      <div class="taksbar-cards flex space-x-10">
        <div class="github-taskcard">
          <TaskBarCard v-if="minimize.githubminimize" name="Github" @click="minimize.githubminimize = false" />
        </div>
        <div class="about-me-taskbarcard">
          <TaskBarCard v-if="minimize.aboutminimize" name="About Me" @click="minimize.aboutminimize = false" />
        </div>
        <div class="network-taskbarcard">
          <TaskBarCard v-if="minimize.networkminimize" name="network" @click="minimize.networkminimize = false" />
        </div>
      </div>

      <div class="flex-1 h-full flex items-center px-3"></div>

    </footer>
  </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import AboutMe from '@/components/AboutMe.vue';
import GithubCard from '@/components/GithubCard.vue';
import TaskBarCard from '@/components/TaskBarCard.vue';
import NetworkCard from '@/components/NetworkCard.vue';
//const props = defineProps<{ open?: boolean }>()
const windows = reactive({
  githubwindow: false,
  aboutwindow: false,
  networkwindow: false
})
const minimize = reactive({
  githubminimize: false,
  aboutminimize: false,
  networkminimize: false
})
function openWindow(window: keyof typeof windows) {
  windows[window] = true;
  //console.log("Window opened:", window.value);
}
function closeWindow(window: keyof typeof windows) {
  windows[window] = false;
}
function minimizeWindow(minimizeKey: keyof typeof minimize) {
  minimize[minimizeKey] = true;
  // Keep window open but hide it with v-if condition
}
</script>

<style scoped>
.task-bar-card {
  display: flex;
  scale: 2;
  align-items: flex-start;

}



button,
input,
optgroup,
select,
textarea {
  font-family: inherit;
  font-feature-settings: inherit;
  font-variation-settings: inherit;
  font-size: 100%;
  font-weight: inherit;
  line-height: inherit;
  letter-spacing: inherit;
  color: inherit;
  margin: 0;
  padding: 0;
}

button,
[role="button"] {
  cursor: pointer;
}

button {
  background: silver;
  background-color: silver;
  background-image: none;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #fff, inset -2px -2px gray, inset 2px 2px #dfdfdf;
}

button {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  min-width: 75px;
  min-height: 23px;
  padding: 0 7px;
  overflow: auto;
}

#start-button[data-astro-cid-e5zwepy2] {
  min-width: 10px;
  max-width: 104px;
  background-image: url("../assets/START_win.png");
  width: 104px;
  background-size: auto 80%;
  background-repeat: no-repeat;
  background-position: .25rem;
  cursor: pointer;
  height: 2.25rem;
  box-shadow: -2px -2px #e0dede, -2px 0 #e0dede, 0 -2px #e0dede, -4px -4px #fff, -4px 0 #fff, 0 -4px #fff, 2px 2px #818181, 0 2px #818181, 2px 0 #818181, 2px -2px #e0dede, -2px 2px #818181, -4px 2px #fff, -4px 4px #000, 4px 4px #000, 4px 0 #000, 0 4px #000, 2px -4px #fff, 4px -4px #000;
}

button {
  -webkit-appearance: button;
  background-color: transparent;
  background-image: none;
}

button .clickable {}

element {
  background-color: #D4D0C8;
  height: 3.5rem;
  width: 100%;
  position: absolute;
  bottom: 0;
  display: flex;
  padding-left: 1rem;
  padding-right: 1rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  justify-content: space-between;
  box-shadow: 0 -2px #fffdfc, 0 -4px #cce9eb;
  z-index: 0;
}

/* desktop teal */
.bg-teal-desktop {
  background-color: #0f7f78;
}

/* icon styling */
.icon-img {
  width: 56px;
  height: 56px;
  object-fit: contain;
  image-rendering: pixelated;
  display: block;
  margin: 0 auto;
  /* slight drop shadow like old icons */
  filter: drop-shadow(0 1px 0 rgba(0, 0, 0, 0.6));
  cursor: pointer;
}

.icon-label {
  margin-top: 6px;
  font-size: 12px;
  color: #ffffff;
  opacity: 0.95;
  line-height: 1;
  font-weight: 500;
  text-align: center;
  /* give a subtle text-shadow to mimic retro look */
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.5);
}
</style>
