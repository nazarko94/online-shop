<template>
  <div class="catalog-cart-item">
    <div class="catalog-cart-item__wrap">
      <img class="catalog-cart-item__image" :src="require('../../assets/img/' + cart_item_data.image)" alt="img">
    </div>
    <div class="catalog-cart-item__info">
      <p>{{cart_item_data.name}}</p>
      <p>{{cart_item_data.price}}</p>
      <p>{{cart_item_data.ariticle}}</p>
    </div>
    <div class="catalog-cart-item__quantity">
      <p>Q-ty:</p>
      <p>
      <span class="catalog-cart-item__btn" @click="decrementItem">-</span>
      {{cart_item_data.quantity}}
      <span class="catalog-cart-item__btn" @click="incrementItem">+</span>
      </p>
    </div>
    <button @click="deleteFromCart" class="deleteFromCart btn">Delete</button>
  </div>
</template>

<script>
  export default {
    name: 'CatalogCartItem',
    components: {},
    props: {
      cart_item_data: {
        type: Object,
        default() {
          return {}
        }
      }
    },
    methods: {
      decrementItem() {
        this.$emit('decrementItem');
      },
      incrementItem() {
        this.$emit('incrementItem');
      },
      deleteFromCart() {
        this.$emit('deleteFromCart')
      }
    }
  }
</script>

<style lang="scss">
  .catalog-cart-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: nowrap;
    padding: 16px;
    margin-bottom: 16px;
    box-shadow: 0 0 8px 0 #e8e8e8;
      &__wrap {
        width: 100px;
        overflow: hidden;
      }
      &__image {
        height: 100%;
        width: 100%;
        object-fit: cover;
        object-position: center;
      }
    &__btn {
      cursor: pointer;
      &:hover {
        opacity: 0.6;
      }
    }  
  }
</style>