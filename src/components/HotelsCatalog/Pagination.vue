<template>
  <div class="pagination">
    <v-pagination v-model="page" :total-visible="3" :length="length"></v-pagination>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
const props = defineProps({
  length: {
    type: Number,
    default: 1,
  },
  injectedPage: {
    type: Number,
    default: 1,
  }
});
const emits = defineEmits(["changePage"]);
const page = ref(1);

watch(() => props.injectedPage, (value) => page.value = value);
watch(page, (value) => emits("changePage", value));

</script>

<style scoped lang="scss"></style>
