<script lang="ts" setup>
import VButton from "@/components/v-button.vue";
import { defineEmits, defineProps, reactive, ref, withDefaults } from "vue";

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

const emit = defineEmits<{
  (e: "select-file", file: never): void;
}>();

const inputRef = ref<HTMLInputElement>();
const file = reactive({
  status: false,
  name: "",
});

function loadFile(event) {
  emit("select-file", event.target.files[0]);
  file.name = event.target.files[0].name;
}
</script>

<template>
  <div class="file-input--wrapper">
    <span v-show="label" class="label">
      {{ label }}
    </span>
    <div class="select-file">
      <label>
        <v-button :disabled="disabled" @click="inputRef.click()">
          <slot>Выбрать файл</slot>
        </v-button>
        <input ref="inputRef" type="file" @change="loadFile" />
      </label>
      <span v-show="file.name.length == 0" class="select">Файл не выбран</span>
      <span class="name">{{ file.name }}</span>
    </div>

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

.select-file {
  display: flex;
  align-items: center;
  gap: 16px;

  span {
    font-size: 14px;
    font-weight: 400;
    line-height: 16px;
    letter-spacing: -0.006em;
    text-align: left;
    color: var(--color-neutral-400);
  }

  span.name {
    color: var(--color-neutral-500);
  }
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
