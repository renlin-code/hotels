<template>
  <button class="simple-button" :class="{ 'simple-button--primary': primary }">
    <slot />
  </button>
</template>

<script setup>
const props = defineProps({
  primary: {
    type: Boolean,
    default: false,
  },
});
</script>

<style scoped lang="scss">
.simple-button {
  width: 100%;
  padding: 17px;
  border-radius: 15px;
  font-weight: 700;
  border: 1px solid $color_light-gray;
  transition: all 0.2s ease-in-out;
  &:hover {
    opacity: 0.7;
  }
  &:active {
    opacity: 1;
  }
  &--primary {
    background: $color_primary;
    color: $color_white;
    border-color: transparent;
  }
}
</style>
