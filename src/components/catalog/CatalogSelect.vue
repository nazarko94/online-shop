<template>
    <div class="catalog-select">
        <p 
            class="catalog-select__title"
            @click="areOptionsVisiable = !areOptionsVisiable"
            >
            {{selected}}
        </p>
        <div 
            class="catalog-select__options"
            v-if="areOptionsVisiable"
        >
            <p  
                class="catalog-select__options-item"
                v-for="option in options"
                :key="option.value"
                @click="selectOption(option)"
            >
                {{option.name}}
            </p>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'CatalogSelect',
        props: {
          options: {
              type: Array,
              default() {
                  return []
              }
          },
          selected: {
            type: String,
            default: '',
        }
        },
        data() {
            return {
              areOptionsVisiable: false,
            }
        },
        methods: {
            selectOption(option) {
                this.$emit('select', option);
                this.areOptionsVisiable = false
            },
            hideSelect() {
                this.areOptionsVisiable = false
            }
        },
        mounted() {
            document.addEventListener('click', this.hideSelect.bind(this), true)
        },
        unmounted() {
            document.removeEventListener('click', this.hideSelect)
        }
    }
</script>

<style lang="scss">
.catalog-select {
  position: relative;
  width: 120px;
  cursor: pointer;
  margin-left: 20px;
  @media (max-width: 348px) {
    margin: 0 auto;
  }
  &__title {
    border: solid 1px #ddd;
  }
  &__options-item {
    margin: 0;
    padding-left: 4px;
    &:hover {
      background-color: #e8e8e8;
    }
  }
  &__options {
    border: solid 1px #ddd;
    position: absolute;
    top: 30px;
    right: 0;
    width: calc(100% - 2px);
    background-color: #fff;
    text-align: left;
  }
}
</style>
