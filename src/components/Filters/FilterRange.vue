<template>
  <div class="filter-range">
    <div class="filter-range__values">
      <div class="filter-range__values-field">от {{ formatter.format(range[0]) }}</div>
      <span>-</span>
      <div class="filter-range__values-field">до {{ formatter.format(range[1]) }}</div>
    </div>
    <v-range-slider
      class="filter-range__slider"
      v-model="range"
      :min="props.minMaxRange[0]"
      :max="props.minMaxRange[1]"
      :step="1"
      strict
      hide-details
      density="compact"
    >
    </v-range-slider>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  minMaxRange: {
    type: Array,
    default: [0, 0],
  },
  resetTrigger: {
    type: Boolean,
    default: false,
  },
});
const emits = defineEmits(["setSelectedRange"]);
const range = ref([props.minMaxRange[0], props.minMaxRange[1]]);

const formatter = new Intl.NumberFormat("ru-RU", {
  minimumIntegerDigits: 1,
  maximumFractionDigits: 0,
  minimumFractionDigits: 0,
  style: "currency",
  currency: "RUB",
});

watch(range, (value) => emits("setSelectedRange", value));
watch(
  () => props.resetTrigger,
  () => (range.value = [props.minMaxRange[0], props.minMaxRange[1]])
);
</script>

<style scoped lang="scss">
.filter-range {
  display: flex;
  flex-direction: column;
  gap: 10px;
  &__values {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    gap: 10px;
    &-field {
      padding: 15px 20px;
      border-radius: 10px;
      border: 1px solid $color_light-gray;
    }
  }
}
</style>
