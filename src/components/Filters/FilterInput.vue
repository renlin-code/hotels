<template>
  <div class="filter-input">
    <v-text-field
      :placeholder="props.placeholder"
      v-model="inputValue"
      type="number"
      step="1"
      min="0"
      density="compact"
    ></v-text-field>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  placeholder: {
    type: String,
    default: "",
  },
  resetTrigger: {
    type: Boolean,
    default: false,
  },
});
const emits = defineEmits(["setInputValue"]);
const inputValue = ref(null);

watch(inputValue, (value) => emits("setInputValue", value));
watch(() => props.resetTrigger, () => (inputValue.value = null));
</script>
