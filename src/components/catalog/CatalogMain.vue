<template>
    <div class="catalog">
        <router-link 
            class="link"
            :to="{name: 'cart'}">
            <div class="catalog__link material-icons"><span class="material-symbols-outlined">
shopping_cart
</span></div>
        </router-link>      
        <h1>Catalog</h1>
        <catalog-notification
            :messages="messages"
        />
        <div class="catalog__filters">
            <catalog-select
                :options="categories"
                @select="sortByCategories"
                :selected="selected"
            />
            <catalog-search/>
        </div>               
        <div class="catalog__list">
            <catalog-item
                v-for="product in filteredProducts"
                :key="product.article"
                :product_data="product"
                @addToCart="addToCart"
            />
        </div>
    </div>
</template>

<script>
import CatalogItem from "./CatalogItem.vue";
import CatalogSelect from "./CatalogSelect.vue";
import { mapActions, mapGetters } from "vuex";
import CatalogNotification from '../notifications/CatalogNotification.vue';
import CatalogSearch from './CatalogSearch.vue';
export default {
  name: "CatalogMain",
  components: {
    CatalogItem,
    CatalogSelect,
    CatalogNotification,
    CatalogSearch,
  },
  data() {
    return {
      categories: [
        { name: "All", value: "All" },
        { name: "Male", value: "M" },
        { name: "Female", value: "F" },
      ],
      selected: "All",
      sortedProducts: [],
      messages: [
        
      ]
    };
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART", 'SEARCH_QUERY']),
    filteredProducts() {
      let vm = this;
      if (this.sortedProducts.length) {
        return this.sortedProducts;
      } else {
        vm.selected = "All";
        return this.PRODUCTS;
      }
    },
  },
  methods: {
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
    addToCart(el) {
      this.ADD_TO_CART(el).
      then(() => {
        let timeStamp = Date.now().toLocaleString();
        this.messages.unshift({name: 'The product has been added to the cart', id: timeStamp})
      })
    },
    sortByCategories(category) {
      let a = this;
      this.PRODUCTS.map(function (item) {
        if (category.name === item.category) {
          a.sortedProducts.push(item);
        }
      });
      if (category) {
        this.sortedProducts = this.sortedProducts.filter(function (e) {
          a.selected = category.name;
          return e.category === category.name;
        });
      }
    },
    filteredByName(value) {
      this.sortedProducts = [...this.PRODUCTS];
      this.selected = 'All';
      if(value) {
        this.sortedProducts = this.sortedProducts.filter((item) => {
          return item.name.toLowerCase().includes(value.toLowerCase());
        })
      } else {
        this.sortedProducts = this.PRODUCTS;
      }
    },
  },
  watch: {
    SEARCH_QUERY() {
      this.filteredByName(this.SEARCH_QUERY);
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API();
    this.filteredByName(this.SEARCH_QUERY);
  },
};
</script>

<style lang="scss">
    .catalog {
        padding-top: 60px;
        @media (max-width: 470px) {
            padding-top: 80px;
        }
        &__list {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }
        &__link {
            position: absolute;
            top: 10px;
            right: 10px;
            padding: 16px;
            border: solid 1px #e8e8e8;
            cursor: pointer;
        }
        &__filters {
            display: flex;
            justify-content: space-between;
            align-items: center;  
            margin-bottom: 10px;   
        }
        &__range {
            width: 150px;
            margin: auto 16px;
            text-align: center;
            position: relative; 
            @media (max-width: 470px) {
                width: 100px;
            }            
            & svg, & input[type=range] {
                position: absolute;
                left: 0;
                bottom: 0;
                width: 100%;
            }
        }
        &__range-values {
            min-width: 80px;
            text-align: left;
        }
    }
    input[type=range]::-webkit-slider-thumb {
        z-index: 2;
        position: relative;
        top: 2px;
        margin-top: -7px;
    }
</style>
