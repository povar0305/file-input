<script lang="ts" setup>
import { defineProps, withDefaults } from "vue";

const props = withDefaults(
  defineProps<{
    disabled: boolean;
  }>(),
  {
    disabled: false,
  }
);
</script>

<template>
  <button :disabled="disabled">
    <slot />
    button
  </button>
</template>

<style scoped>
button {
  padding: 12px;
  font-size: 14px;
  font-family: "Inter", sans-serif;
  font-weight: 400;
  line-height: 16px;
  letter-spacing: -0.006em;
  text-align: left;
  color: var(--color-neutral-700);
  border-radius: 12px;
  background: var(--color-base-white);
  border: 1px solid var(--color-neutral-200);
  box-shadow: 0 3px 7px -3px #00000014;
  transition: all ease-out 300ms;
}

button:not([disabled]):hover {
  background: var(--color-neutral-100);
  border-color: var(--color-neutral-300);
  box-shadow: 0 4px 8px 0 #00000005;
}

button:not([disabled]):active {
  background: var(--color-neutral-200);
}

button:not([disabled]) {
  cursor: pointer;
}

button[disabled] {
  border-color: var(--color-neutral-200);
  color: var(--color-neutral-400);
}
</style>
