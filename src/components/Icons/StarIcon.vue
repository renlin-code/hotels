<template>
  <svg
    width="14"
    height="14"
    viewBox="0 0 14 14"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M7 11.2513L11.3262 14L10.178 8.82L14 5.33467L8.96707 4.88533L7 0L5.03293 4.88533L0 5.33467L3.82204 8.82L2.67384 14L7 11.2513Z"
      :fill="active ? '#FFA900' : '#D7D7D7'"
    />
  </svg>
</template>

<script setup>
    const props = defineProps({
        active: {
            type: Boolean,
            default: false
        }
    })
</script>
