<script setup>
import ListItem from "./ListItem.vue";
</script>

<template>
  <div class="items-container">
    <ListItem name="Projects:" text="Create project" />
    <ListItem name="Tasks:" text="Create task" />
  </div>
</template>

<style scoped>
.items-container {
  display: flex;
  flex-direction: column;
  gap: 72px;
}
</style>
