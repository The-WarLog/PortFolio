<template>
  <div class="taskbar-card">
    <div class="taks-card">
      <button class="default">{{ props.name }}</button>
    </div>
  </div>

</template>

<script setup lang="ts">
const props = defineProps<{
  name?: string;
  taskbarclick?: boolean;
}>();
//const emit = defineEmits();

</script>
<style scoped>
.default {
  scale: 1.4;
}
</style>
