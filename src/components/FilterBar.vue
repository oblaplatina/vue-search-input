<template>
    <div class="filter-bar">
        <select v-model="selectedCategory" @change="onCategoryChange">
            <option value="">All categories</option>
            <option v-for="category in categories" :key="category.slug" :value="category.slug">
                {{ category.name }}
            </option>
        </select>
    </div>
</template>

<script setup>
import { ref } from "vue";

defineProps({
    categories: {
        type: Array,
        required: true,
    }
});

const emit = defineEmits(["categorySelect"]);

const selectedCategory = ref("");

function onCategoryChange() {
    emit("categorySelect", selectedCategory.value);
}
</script>

<style scoped>
.filter-bar {
    display: flex;
    justify-content: center;
}

.filter-bar select {
    padding: 10px;
    margin: 20px 0;
    border-radius: 28px;
}
</style>