<template>
  <div class="filter-search">
    <v-autocomplete
      clearable
      chips
      label="Поиск стран"
      no-data-text="К сожалению, по вашему запросу ничего не найдено :("
      :items="props.items"
      :multiple="props.items.length > 1"
      v-model="selectedItems"
      density="compact"
      thumb-label="always"
    ></v-autocomplete>
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
const selectedItems = ref(null);

watch(selectedItems, (value) => emits("setSelectedItems", value));
watch(() => props.resetTrigger, () => (selectedItems.value = null));
</script>
