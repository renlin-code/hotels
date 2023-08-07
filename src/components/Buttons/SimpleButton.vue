<template>
  <button
    class="simple-button"
    :class="{
      'simple-button--primary': type === 'primary',
      'simple-button--secondary': type === 'secondary',
      'simple-button--opaque-purple': type === 'opaque-purple',
      'simple-button--opaque-green': type === 'opaque-green',

      'simple-button--sm': size === 'sm',
      'simple-button--md': size === 'md',
      'simple-button--lg': size === 'lg',
    }"
  >
    <slot class="simple-button__slot" />
  </button>
</template>

<script setup>
const props = defineProps({
  type: {
    type: String,
    default: "primary",
  },
  size: {
    type: String,
    default: "md",
  },
});
</script>

<style scoped lang="scss">
.simple-button {
  width: 100%;
  border-radius: 15px;
  transition: all 0.2s ease-in-out;
  &:hover {
    opacity: 0.7;
  }
  &:active {
    opacity: 1;
  }
  &__slot {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }
  &--primary {
    background: $color_primary;
    color: $color_white;
    border-color: transparent;
  }
  &--secondary {
    border: 1px solid $color_light-gray;
    background: $color_white;
    color: $color_black;
  }
  &--opaque-purple {
    background: rgba($color_primary, 0.1);
    color: $color_primary;
  }
  &--opaque-green {
    background: rgba($color_green, 0.1);
    color: $color_green;
  }

  &--sm {
    padding: 10px;
    font-size: 14px;
    font-weight: 400;
  }
  &--md {
    padding: 14px;
    font-size: 16px;
    font-weight: 700;
  }
  &--lg {
    padding: 17px;
    font-size: 16px;
    font-weight: 700;
  }
}
</style>
