<script lang="ts" setup>
import VButton from "@/components/v-button.vue";
import { defineEmits, defineProps, reactive, ref, withDefaults } from "vue";

withDefaults(
  defineProps<{
    disabled?: boolean;
    label?: string;
    hint?: string;
    error?: string;
    multiple?: boolean;
    accept?: string;
  }>(),
  {
    disabled: false,
    multiple: false,
    accept: "image/*",
  }
);

const emit = defineEmits<{
  (e: "select-file", uploadFile: any): void;
  (e: "succes-send", data: any): void;
  (e: "error-send", error: any): void;
  (e: "cancellation"): void;
  (e: "delete"): void;
}>();

const inputRef = ref<HTMLInputElement>();
const file = reactive({
  name: "",
});
const showLoader = ref(false);

async function uploadFile(event: Event) {
  const formData = new FormData();
  file.name = "";
  let i = 0;
  let namesFile = [];
  while (i < event.target.files.length) {
    // выводит 0, затем 1, затем 2
    console.log(event.target.files[i]);
    formData.append("file", event.target.files[i]);
    emit("select-file", event.target.files[i]);
    namesFile.push(event.target.files[i].name);
    i++;
  }
  file.name = namesFile.join(", ");

  //
  // headers: {
  //   'Content-Type': 'text/plain'
  // },

  try {
    showLoader.value = true;
    const response = await fetch("/upload", { method: "POST", body: formData });
    const data = await response.json();
    emit("succes-send", data);
    showLoader.value = false;
  } catch (err) {
    showLoader.value = false;
    emit("error-send", err);
  }
}

function selectFile() {
  console.log(file.name.length);
  if (file.name.length == 0) {
    inputRef.value.click();
  } else {
    if (showLoader.value) {
      emit("cancellation");
    } else {
      file.name = "";
      emit("delete");
    }
  }
}
</script>

<template>
  <div class="file-input--wrapper">
    <span v-show="label" class="label">
      {{ label }}
    </span>
    <div class="select-file">
      <label>
        <v-button :disabled="disabled" @click="selectFile">
          <slot>
            <span v-show="file.name == 0">
              Выбрать файл<template v-if="multiple">ы</template>
            </span>
            <span v-show="!showLoader && file.name.length > 0">Удалить</span>
            <span v-show="showLoader">Отменить</span>
          </slot>
        </v-button>
        <input
          ref="inputRef"
          :accept="accept"
          :multiple="multiple"
          type="file"
          @change="uploadFile"
        />
      </label>
      <span v-show="file.name.length == 0" class="select">Файл не выбран</span>
      <span class="name">
        <img
          v-show="showLoader"
          alt="Иконка лоадера"
          class="loader"
          src="@/assets/icons/icon-loader.svg"
        />
        {{ file.name }}</span
      >
    </div>
    <span v-show="hint" class="hint">{{ hint }}</span>
    <span v-show="error" class="error">{{ error }}</span>
  </div>
</template>

<style scoped>
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.loader {
  animation: 0.5s linear infinite rotate;
  transition: 0.3s;
}

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
