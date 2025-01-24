<template>
  <div>
    <SearchBar :onSearchInput="handleSearch" />
    <FilterBar :categories="categories" :onCategorySelect="handleCategoryChange" />
    <ProductList :products="paginatedProducts" />
    <ProductPagination :currentPage="currentPage" :totalPages="totalPages" :onPageChange="handlePageChange" />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import FilterBar from "./components/FilterBar.vue";
import ProductList from "./components/ProductList.vue";
import ProductPagination from "./components/ProductPagination.vue";

export default {
  components: {
    SearchBar,
    FilterBar,
    ProductList,
    ProductPagination,
  },
  data() {
    return {
      products: [],
      categories: [],
      searchQuery: "",
      selectedCategory: "",
      currentPage: 1,
      productsPerPage: 8,
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter((product) => {
        const matchesSearch = product.title
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase());
        const matchesCategory =
          !this.selectedCategory || product.category === this.selectedCategory;
        return matchesSearch && matchesCategory;
      });
    },
    paginatedProducts() {
      const start = (this.currentPage - 1) * this.productsPerPage;
      const end = start + this.productsPerPage;
      return this.filteredProducts.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.filteredProducts.length / this.productsPerPage);
    },
  },
  mounted() {
    fetch("https://dummyjson.com/products")
      .then((response) => response.json())
      .then((data) => {
        this.products = data.products;
      })
      .catch((error) => {
        console.error("Ошибка загрузки продуктов:", error);
      });

    fetch("https://dummyjson.com/products/categories")
      .then((response) => response.json())
      .then((data) => {
        console.log("Категории из API:", data);
        this.categories = data.map((category) => ({
          name: category.name,
          slug: category.slug,
        }));
      })
      .catch((error) => {
        console.error("Ошибка загрузки категорий:", error);
      });
  },
  methods: {
    handleSearch(query) {
      this.searchQuery = query;
      this.currentPage = 1;
    },
    handleCategoryChange(category) {
      this.selectedCategory = category;
      this.currentPage = 1;
    },
    handlePageChange(page) {
      this.currentPage = page;
    },
  },
};
</script>

<style>
body {
  max-width: 1050px;  
  margin: 0 auto;
  padding: 0;
}
</style>
