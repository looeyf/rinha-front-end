<script setup lang="ts"></script>

<template>
  <section class="empty-state container">
    <h1>JSON Tree Viewer</h1>
    <p>Simple JSON Viewer that runs completely on-client. No data exchange </p>
    <slot name="action"></slot>
  </section>
</template>

<style scoped>
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  height: 100%;
}

h1 {
  font-size: 3rem;
}

p {
  font-size: 1.5rem;
}
</style>