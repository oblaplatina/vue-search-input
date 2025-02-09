<template>
  <div>
    <SearchBar @searchInput="handleSearch" />
    <FilterBar :categories="categories" :onCategorySelect="handleCategoryChange" />
    <ProductList :products="paginatedProducts" />
    <ProductPagination :currentPage="currentPage" :totalPages="totalPages" :onPageChange="handlePageChange" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import SearchBar from "./components/SearchBar.vue";
import FilterBar from "./components/FilterBar.vue";
import ProductList from "./components/ProductList.vue";
import ProductPagination from "./components/ProductPagination.vue";

const products = ref([]);
const categories = ref([]);
const searchQuery = ref("");
const selectedCategory = ref("");
const currentPage = ref(1);
const productsPerPage = ref(8);

const filteredProducts = computed(() => {
  return products.value.filter((product) => {
    const matchesSearch = product.title
      .toLowerCase()
      .includes(searchQuery.value.toLowerCase());
    const matchesCategory =
      !selectedCategory.value || product.category === selectedCategory.value;
    return matchesSearch && matchesCategory;
  });
});

const paginatedProducts = computed(() => {
  const start = (currentPage.value - 1) * productsPerPage.value;
  const end = start + productsPerPage.value;
  return filteredProducts.value.slice(start, end);
});

const totalPages = computed(() => {
  return Math.ceil(filteredProducts.value.length / productsPerPage.value);
});

function handleSearch(query) {
  searchQuery.value = query;
  currentPage.value = 1;
}

function handleCategoryChange(category) {
  selectedCategory.value = category;
  currentPage.value = 1;
}

function handlePageChange(page) {
  currentPage.value = page;
}

onMounted(() => {
  fetch("https://dummyjson.com/products")
    .then((response) => response.json())
    .then((data) => {
      products.value = data.products;
    })
    .catch((error) => {
      console.error("Ошибка загрузки продуктов:", error);
    });

  fetch("https://dummyjson.com/products/categories")
    .then((response) => response.json())
    .then((data) => {
      categories.value = data.map((category) => ({
        name: category.name,
        slug: category.slug,
      }));
    })
    .catch((error) => {
      console.error("Ошибка загрузки категорий:", error);
    });
});
</script>

<style>
body {
  max-width: 1050px;
  margin: 0 auto;
  padding: 0;
}
</style>
