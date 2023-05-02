<template>
  <div class="catalog-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="catalog__link">Back to catalog</div>
    </router-link>
    <h1>Cart</h1>  
    <p v-if="!CART.length">There are no products in the cart...</p>
    <cart-item-wrapper
      v-if="CART.length"
      :cart_data="CART"
    />
  </div>
</template>

<script>
import CartItemWrapper from './CartItemWrapper.vue';
import {mapGetters} from 'vuex';
  export default {
    name: 'CatalogCart',
    components: {
      CartItemWrapper,
    },
    computed: {
      ...mapGetters([
        'CART',
      ])
    },
  }
</script>

<style lang="scss">
  .catalog__link {
    color: #2c3e50;
    &:hover {
      opacity: 0.8;
    }
  }
</style>