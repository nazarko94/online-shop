<template>
  <form class="catalog-search">
    <i class="catalog-search__icon material-icons" @click="$event => searchByName(searchQuery)">search</i>
    <input 
      name="query"
      placeholder="Search..."
      class="catalog-search__input"
      v-model="searchQuery"
    >
    <i 
      class="catalog-search__clear material-icons"
      @click="$event => clearSearch()"
    >clear</i>
  </form>
</template>

<script>
import { mapActions } from 'vuex'
  export default {
    name: 'CatalogSearch',
    data() {
      return {
        searchQuery: '',
      }
    },
    methods: {
      ...mapActions([
        'GET_SEARCH_QUERY'
      ]),
      searchByName(name) {
        this.GET_SEARCH_QUERY(name);
      },
      clearSearch() {
        this.searchQuery = '';
        this.GET_SEARCH_QUERY();
      }
    }
  }
</script>

<style lang="scss">
  .catalog-search {
    position: relative;
    &__icon, &__clear {
      position: absolute;
      color: #2c3e50;
      cursor: pointer;
      &:hover {
        opacity: 0.7;
      }
    }
    &__icon {
        top: 3px;
        left: 5px;
        border-right: 1px solid #e8e8e8;
      }
      &__clear {
        top: 3px;
        right: 25px;
      }
      &__input {
        border: 1px solid #e8e8e8;
        margin-right: 24px;
        padding: 6px 0 6px 35px;
        width: 200px;
      }
  }
</style>