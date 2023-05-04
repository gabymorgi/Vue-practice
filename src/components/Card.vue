<script setup lang="ts">
  defineProps<{
    title?: string
  }>()
</script>

<template>
  <div class="card-container">
    <div v-if="title" class="card-title">{{ title }}</div>
    <div class="card-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
  .card-container {
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .card-container > * {
    padding: 1rem;
  }
  .card-title {
    font-weight: bold;
    border-bottom: 1px solid #ccc;
  }
</style>