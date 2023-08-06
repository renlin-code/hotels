<template>
  <div class="filter-checkboxes">
    <v-checkbox
      v-for="item in items"
      :label="item"
      :value="item"
      v-model="selected"
      density="compact"
    ></v-checkbox>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
const props = defineProps({
  items: {
    type: Array,
    default: [],
  },
  resetTrigger: {
    type: Boolean,
    default: false,
  },
});
const emits = defineEmits(["setSelectedItems"]);
const selected = ref([]);

watch(selected, (value) => emits("setSelectedItems", value));
watch(() => props.resetTrigger, () => (selected.value = []));
</script>
