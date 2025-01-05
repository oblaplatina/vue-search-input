<template>
  <div>
    <SearchBar />
    <ProductList />
    <FilterBar />
    <ProductPagination />
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar.vue';
import ProductList from '@/components/ProductList.vue'
import FilterBar from '@/components/FilterBar.vue';
import ProductPagination from '@/components/ProductPagination.vue';

export default {
  components: {
    SearchBar,
    ProductList,
    FilterBar,
    ProductPagination
  }
}
</script>

<style></style>
