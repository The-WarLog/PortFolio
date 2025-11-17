<script setup lang="ts">
import { ref } from 'vue'
//import Icon from './Icon.vue'; // <-- Import the Icon component

// You'll need to find an icon image and put it in your /public folder
const docIcon = '/icons/doc-icon-95.png';

const projects = ref([
  { name: 'Summize', img: docIcon },
  { name: 'Notion2Canvas', img: docIcon },
  { name: 'PGPCord', img: docIcon },
  { name: 'IMDB Frontend', img: docIcon }
])
</script>

<template>
  <div class="w-96"
    style="background: #c0c0c0; border-top: 2px solid #ffffff; border-left: 2px solid #ffffff; border-right: 2px solid #808080; border-bottom: 2px solid #808080; padding: 3px;">
    <div class="flex items-center justify-between px-2 py-1"
      style="background: linear-gradient(to right, #000080, #1084d0);">
      <span class="font-bold text-white">Projects</span>

      <div class="flex space-x-1">
        <button class="w-4 h-4"
          style="background: #c0c0c0; border-top: 1px solid #fff; border-left: 1px solid #fff; border-right: 1px solid #000; border-bottom: 1px solid #000;">_</button>
        <button class="w-4 h-4"
          style="background: #c0c0c0; border-top: 1px solid #fff; border-left: 1px solid #fff; border-right: 1px solid #000; border-bottom: 1px solid #000;">[]</button>
        <button class="w-4 h-4"
          style="background: #c0c0c0; border-top: 1px solid #fff; border-left: 1px solid #fff; border-right: 1px solid #000; border-bottom: 1px solid #000;">X</button>
      </div>
    </div>

    <div class="p-4 flex flex-wrap gap-4"
      style="border-top: 2px solid #808080; border-left: 2px solid #808080; border-right: 2px solid #ffffff; border-bottom: 2px solid #ffffff;">
      <Icon v-for="project in projects" :key="project.name" :name="project.name" :imageSrc="project.img" />
    </div>
  </div>
</template>
