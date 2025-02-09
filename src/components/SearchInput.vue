<template>
    <input :value="inputValue" @input="handleInput" :placeholder="placeholder" class="search-input" />
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
    modelValue: {
        type: String,
        default: '',
    },
    placeholder: {
        type: String,
        default: 'Search...',
    },
    debounceDelay: {
        type: Number,
        default: 500,
    },
});

const emit = defineEmits(['update:modelValue']);

const inputValue = ref(props.modelValue);

watch(
    () => props.modelValue,
    (newVal) => {
        inputValue.value = newVal;
    }
);

function debounce(func, delay) {
    let timeout;
    return function (...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func(...args), delay);
    };
}

const debouncedEmit = debounce((value) => {
    emit('update:modelValue', value);
}, props.debounceDelay);

function handleInput(event) {
    inputValue.value = event.target.value;
    debouncedEmit(inputValue.value);
}
</script>

<style scoped>
.search-input {
    padding: 10px;
    margin-top: 20px;
    width: 100%;
    max-width: 400px;
    border-radius: 28px;
}
</style>