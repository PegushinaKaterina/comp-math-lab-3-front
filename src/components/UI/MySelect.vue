<template>
    <select :value="modelValue" class="select elementForm" @change="changeOption">
        <option
                v-for="option in options"
                :key="option.value"
                :value="option.value"
                class="elementForm"
        >
            {{ option.name }}
        </option>
    </select>
</template>

<script>
export default {
    name: "my-select",
    props: {
        modelValue: {
            type: Number,
        },
        options: {
            type: Array,
            default: () => [],
        },
    },
    methods: {
        changeOption(event) {
            this.$emit("update:modelValue", Number(event.target.value));
        },
    },
};
</script>

<style scoped>
.select {
    width: 100%;
    color: black;
    background-color: #836c7b;
    padding: 7px;
    border: 1.5px solid black;
    font-size: var(--element-form-text-size);
}
</style>
