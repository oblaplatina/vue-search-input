<template>
    <div class="search-bar">
        <SearchInput v-model="searchText" placeholder="Search products..." :debounceDelay="500" />
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import SearchInput from './SearchInput.vue';

const searchText = ref('');

const emit = defineEmits(['searchInput']);

watch(searchText, (newVal) => {
    emit('searchInput', newVal);
});
</script>

<style scoped>
.search-bar {
    display: flex;
    justify-content: center;
}
</style>