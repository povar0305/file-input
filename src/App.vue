<template>
  <div class="wrapper-inputs">
    <file-input />
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
