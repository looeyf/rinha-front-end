<script setup lang='ts'>
import { ref, watch } from 'vue';

const file = ref<File>();
const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement;
  if (!target.files) return;
  file.value = target.files[0];
};

const parsedJson = ref<any>({});
const parseJsonFile = (file: File) => {
  return new Promise((resolve, reject) => {
    const fileReader = new FileReader();
    fileReader.onload = (event) => resolve(JSON.parse(event.target?.result as string || ''));
    fileReader.onerror = error => reject(error);
    fileReader.readAsText(file);
  });
};

watch(file, async () => {
  if (!file.value) return;
  const result = await parseJsonFile(file.value);
  parsedJson.value = result;
});
</script>

<template>
  <section class="empty-state container">
    <h1>JSON Tree Viewer</h1>
    <p>Simple JSON Viewer that runs completely on-client. No data exchange </p>
    <div class="file-uploader">
      <label tabindex="1" for="jsonFile">Load JSON</label>
      <input @change="handleFileChange" type="file" id="jsonFile" accept=".json" />
    </div>
  </section>

  <pre>
    {{ parsedJson }}
  </pre>
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