<template>
    <div class="pagination">
        <button @click="prevPage" :disabled="currentPage === 1">Back</button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
</template>

<script setup>
const props = defineProps({
    currentPage: {
        type: Number,
        required: true,
    },
    totalPages: {
        type: Number,
        required: true,
    }
});

const emit = defineEmits(["pageChange"]);

function prevPage() {
    if (props.currentPage > 1) {
        emit("pageChange", props.currentPage - 1);
    }
}

function nextPage() {
    if (props.currentPage < props.totalPages) {
        emit("pageChange", props.currentPage + 1);
    }
}
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