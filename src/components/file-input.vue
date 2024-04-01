<script lang="ts" setup>
import VButton from "@/components/v-button.vue";
import { ref } from "vue";

const inputRef = ref<HTMLInputElement>();
</script>

<template>
  <label
    >File
    <v-button disabled @click="inputRef.click()"> text</v-button>
    <input ref="inputRef" type="file" />
  </label>
</template>

<style scoped>
input {
  position: absolute;
  left: -9999px;
}
</style>
