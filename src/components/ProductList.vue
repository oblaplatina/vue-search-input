<template>
    <div class="product-list">
        <div v-for="product in products" :key="product.id" class="product-card">
            <h3>{{ product.title }}</h3>
            <p>{{ product.description }}</p>
            <p>Price: ${{ product.price }}</p>
        </div>
    </div>
</template>

<script setup>
defineProps({
    products: {
        type: Array,
        required: true,
    }
});
</script>

<style scoped>
.product-list {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: center;
}

.product-card {
    border: 1px solid #ddd;
    padding: 10px;
    max-width: 200px;
    height: 300px;
    background-color: #f9f9f9;
    border-radius: 28px;
}
</style>