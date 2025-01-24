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

<script>
export default {
    name: "FilterBar",
    props: ["categories", "onCategorySelect"],
    data() {
        return {
            selectedCategory: "",
        };
    },
    methods: {
        onCategoryChange() {
            this.onCategorySelect(this.selectedCategory);
        },
    },
};
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