<template>
    <button class="simple-button">
        <slot />
    </button>
</template>

<script setup>

</script>

<style scoped lang="scss">
    .simple-button {
        width: 100%;
        padding: 17px;
        background: green;
        border-radius: 15px;
    }
</style>