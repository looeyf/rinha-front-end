<script setup lang='ts'>
defineProps<{
  data: any,
}>();
</script>

<!-- TODO: Show the result object as the proposed UI -->
<template>
  <pre>
    {{ data }}
  </pre>
</template>

<style scoped></style>