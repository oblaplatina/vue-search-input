<template>
    <div class="pagination">
        <button @click="prevPage" :disabled="currentPage === 1">Назад</button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Вперед</button>
    </div>
</template>

<script>
export default {
    name: "ProductPagination",
    props: ["currentPage", "totalPages", "onPageChange"],
    methods: {
        prevPage() {
            if (this.currentPage > 1) {
                this.onPageChange(this.currentPage - 1);
            }
        },
        nextPage() {
            if (this.currentPage < this.totalPages) {
                this.onPageChange(this.currentPage + 1);
            }
        },
    },
};
</script>

<style scoped>
.pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    margin-top: 50px;
}

.pagination button {
    padding: 10px;
    border: 1px solid #ddd;
    background-color: #f9f9f9;
    cursor: pointer;
    border-radius: 28px;
}

.pagination button:disabled {
    background-color: #eee;
    cursor: not-allowed;
}
</style>