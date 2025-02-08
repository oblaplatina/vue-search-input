<template>
    <div class="search-bar">
        <input type="text" v-model="searchQuery" @input="onInput" placeholder="Search products" />
    </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["searchInput"]);

const searchQuery = ref("");

function debounce(func, delay) {
    let timeout;
    return function (...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), delay);
    };
}

const onInput = debounce(() => {
    emit("searchInput", searchQuery.value);
}, 500);
</script>

<style scoped>
.search-bar {
    display: flex;
    justify-content: center;
}

.search-bar input {
    padding: 10px;
    width: 100%;
    max-width: 400px;
    margin: 10px auto;
    border-radius: 28px;
}
</style>