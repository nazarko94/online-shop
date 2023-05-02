<template>
  <div id="app">
    <catalog-wrapper/>
  </div>
</template>

<script>
import CatalogWrapper from "@/components/catalog/CatalogWrapper.vue";

export default {
  name: 'App',
  components: {
    CatalogWrapper,
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
  }
</style>
