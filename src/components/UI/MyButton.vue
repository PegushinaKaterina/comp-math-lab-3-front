<template>
    <button class="button elementForm">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: "my-button",
};
</script>

<style scoped>
.button {
    width: var(--button-size);
    margin-top: 20px;
    padding: var(--button-padding-size);
    background-color: #d59e6a;
    border: 1.5px solid black;
    font-size: var(--element-form-text-size);
}
</style>
