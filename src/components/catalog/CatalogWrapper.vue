<template>
  <div class="catalog-wrapper">
    <router-view></router-view>

  </div>
</template>

<script>
  import {mapGetters} from 'vuex';

  export default {
    name: 'CatalogWrapper',
    props: {},
    data() {
      return {
        
      }
    },
    computed: {
      ...mapGetters([
        'CART',
      ])
    },
    methods: {},
    watch: {},
  }
</script>

<style lang="scss">
  .catalog-wrapper {
    max-width: 900px;
    margin: 0 auto;
    text-align: center;
  }
</style>