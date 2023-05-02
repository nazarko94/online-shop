<template>
  <div class="catalog-popup__wrapper" ref="popup_wrapper">
    <div class="catalog-popup">
      <div class="catalog-popup__header">
        <span>{{popupTitle}}</span>
        <span>
          <i 
            class="material-icons catalog-popup__icon"
            @click="closePopup"
          >
            close
          </i>
        </span>
      </div>
      <div class="catalog-popup__content">
        <slot></slot>
      </div>
      <div class="catalog-popup__footer">
        <button 
          class="btn catalog-popup__close"
          @click="closePopup"
          >
          Close
        </button>
        <button 
          class="btn"
          @click="rightBtnAction"
        >
          {{rightBtnPopup}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'CatalogPopup',
    methods: {
      closePopup() {
        this.$emit('closePopup');
      },
      rightBtnAction() {
        this.$emit('rightBtnAction')
      }
    },
    props: {
      rightBtnPopup: {
        type: String,
        default: 'Ok',
      },
      popupTitle: {
        type: String,
        default: 'Popup name'
      }
    },
    mounted() {
      let c = this;
      document.addEventListener('click', function(item) {
        if(item.target === c.$refs['popup_wrapper']) {
          c.closePopup();
        }
      })
    }
  }
</script>

<style lang="scss">
   .catalog-popup {
        padding: 16px;
        position: fixed;
        top: 250px;
        width: 400px;
        box-shadow: 0 0 16px 0 #e8e8e8;
        left: calc(50% - 200px);
        z-index: 333;
        background-color: #fff;
        @media (max-width: 768px) {
            width: 300px;
            left: calc(50% - 166px);
        }
        @media (max-width: 550px) {
            width: 260px;
            left: calc(50% - 146px);
        }
        &__wrapper {
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: rgba(64, 64, 64, 0.4);
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            z-index: 433;
            height: 200%;
        }
        &__header, &__footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        &__content {
            display: flex;
            justify-content: center;
            align-items: center;
        }
        &__icon {
            cursor: pointer;
            &:hover {
                opacity: 0.6;
            }
        }
        &__btn {
            padding: 8px;
            color: #fff;
            background-color: #000;
        }
        &__close.btn {
            padding: 8px;
            color: #fff;
            background-color: #f00;
            &:hover {
                opacity: 0.8;
            }
        }
   }
</style>