<script setup lang="ts">
import { ref, watch } from 'vue';
import EmptyState from './components/EmptyState.vue';
import FileInput from './components/FileInput.vue';
import JsonViewer from './components/JsonViewer.vue';

const file = ref<File>();
const handleFileChange = (event: Event) => {
  const target = event.target as HTMLInputElement;
  if (!target.files) return;
  file.value = target.files[0];
};

const parsedJson = ref<any>({});
const parseJsonFile = (file: File) => {
  // TODO: maybe use a web worker to handle this execution and add a loading indicator
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
  <main>
    <!-- TODO: Add error state -->
    <EmptyState v-if="!parsedJson">
      <template #action>
        <FileInput @on-change="handleFileChange" />
      </template>
    </EmptyState>

    <JsonViewer v-else :data="parsedJson" />
  </main>
</template>

<style scoped>
main {
  width: 100vw;
  height: 100vh;
  min-height: 100vh;
}
</style>
