<script lang="ts" setup>
import VButton from "@/components/v-button.vue";
import { defineProps, ref, withDefaults } from "vue";

withDefaults(
  defineProps<{
    disabled?: boolean;
    label?: string;
    hint?: string;
    error?: string;
  }>(),
  {
    disabled: false,
  }
);
const inputRef = ref<HTMLInputElement>();
</script>

<template>
  <div class="file-input--wrapper">
    <span v-show="label" class="label">
      {{ label }}
    </span>
    <label>
      <v-button :disabled="disabled" @click="inputRef.click()">
        <slot>Выбрать файл</slot>
      </v-button>
      <input ref="inputRef" type="file" />
    </label>
    <span v-show="hint" class="hint">{{ hint }}</span>
    <span v-show="error" class="error">{{ error }}</span>
  </div>
</template>

<style scoped>
input {
  position: absolute;
  left: -9999px;
}

.file-input--wrapper {
  display: flex;
  flex-direction: column;
  justify-content: start;
  font-family: "Inter", sans-serif;
}

label {
  display: flex;
}

span {
  font-size: 13px;
  line-height: 15px;
  text-align: left;
}

span.label {
  margin-bottom: 12px;
  font-weight: 500;
  color: var(--color-neutral-900);
}

span.hint {
  font-weight: 400;
  margin-top: 8px;
  color: var(--color-neutral-500);
}

span.error {
  font-weight: 400;
  margin-top: 8px;
  color: var(--color-error-500);
}
</style>
