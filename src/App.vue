<template>
  <div class="wrapper-inputs">
    <file-input
      hint="Hint text"
      label="Label"
      @select-file="console.log('select', $event)"
      @error-send="console.log('error-send', $event)"
    />
    <file-input
      accept="video/*"
      hint="Выбор только видео файлов"
      label="Label"
      @select-file="console.log('select', $event)"
      @error-send="console.log('error-send', $event)"
    />
    <file-input
      hint="Выбор нескольких файлов"
      label="Label"
      multiple
      @select-file="console.log('select', $event)"
      @error-send="console.log('error-send', $event)"
    />
    <file-input
      error="Error text"
      label="Label"
      @select-file="console.log('select', $event)"
      @error-send="console.log('error-send', $event)"
    />
    <file-input disabled label="Задизаблено" />
  </div>
</template>

<script lang="ts" setup>
import FileInput from "@/components/file-input.vue";
</script>

<style>
@import url("/src/assets/main.css");

#app {
  font-family: "Inter";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 24px;
}

.wrapper-inputs {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>
