<script setup lang='ts'>
defineEmits<{
  (e: 'onChange', event: Event): void
}>()
</script>

<template>
  <div class="file-uploader">
    <label tabindex="1" for="jsonFile">Load JSON</label>
    <input @change="(e) => $emit('onChange', e)" type="file" id="jsonFile" accept=".json" />
  </div>
</template>

<style scoped>
.file-uploader input {
  display: none;
}

.file-uploader label {
  background: linear-gradient(180deg, #E4E4E4 0%, #F7F7F7 100%);
  border-radius: 5px;
  padding: 0.375rem 0.75rem;
  font-size: 16px;
  font-weight: 500;
  opacity: 0.7;
  border: 1px solid var(--black);
  cursor: pointer;
}

.file-uploader label:focus {
  outline: 2px solid var(--black);
}
</style>