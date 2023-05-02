<template>
  <div class="catalog-item">
    <catalog-popup
      v-if="isPopupVisiable"
      rightBtnPopup="Add to Cart"
      @closePopup="closePopup"
      :popup-title="product_data.name"
      @rightBtnAction="addToCart"
    >
      <div class="catalog-item__popup">
        <div class="catalog-item__image-wrap">
          <img class="catalog-item__image" :src="require('../../assets/img/' + product_data.image)" alt="img">
        </div>
        <div class="catalog-item__content">
          <p class="catalog-item__name">{{product_data.name}}</p>
          <p class="catalog-item__price">{{product_data.price}} UAH</p>
          <p class="catalog-item__price">{{product_data.category}}</p>
        </div>
      </div>
    </catalog-popup>
    <div class="catalog-item__image-wrap">
      <img class="catalog-item__image" :src="require('../../assets/img/' + product_data.image)" alt="img">
    </div>
    <p class="catalog-item__name">{{product_data.name}}</p>
    <p class="catalog-item__price">{{product_data.price}} UAH</p>
    <div class="catalog-item__btns">
      <button 
        class="catalog-item__show-info btn"
        @click="showPopup"
      >
        Show info
      </button>
      <button
      class="catalog-item__btn btn"
      @click="addToCart"
      >Add to cart
      </button>
    </div>
  </div>
</template>

<script>
import CatalogPopup from '../popup/CatalogPopup.vue';

  export default {
    name: 'CatalogItem',
    components: {
      CatalogPopup,
    },
    data() {
      return {
        isPopupVisiable: false,
      }
    },
    props: {
      product_data: {
        type: Object,
        default() {
          return {}
        } 
      }
    },
    methods: {
      addToCart() {
        this.$emit('addToCart', this.product_data);
      },
      showPopup() {
        this.isPopupVisiable = true;
      },
      closePopup() {
        this.isPopupVisiable = false;
      },
    }
  }
</script>

<style lang="scss">
  .catalog-item {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e8e8e8;
    padding: 16px;
    margin: 16px;
    min-width: 150px;
    @media (max-width: 470px) {
      padding: 8px;
    }
    &__image-wrap {
      width: 100px;
      overflow: hidden;
      margin: 0 auto;
    }
    &__image {
      object-fit: cover;
      object-position: center;
      width: 100%;
      height: 100%;
    }
    &__show-info.btn {
      background-color: #2c3e50;
    }
    &__btns {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: stretch;
      margin: 0 18px;
      gap: 8px;
    }
    &__popup {
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
    &__content {
      padding-left: 8px;
    }
  }
  .btn {
      cursor: pointer;
      background-color: rgb(26, 117, 8);
      border: none;
      padding: 8px;
      border-radius: 4px;
      color: #fff;
      &:hover {
        opacity: 0.8;
      }
      @media (max-width: 470px) {
        padding: 8px;
        font-size: 14px;
      }
    }
</style>