<template>
  <div class="catalog-notification">
    <transition-group
      name="transition-animate"
      class="catalog-notification__list"
      tag="div"
    >
      <div 
        class="catalog-notification__content"
        v-for="message in messages"
        :key="message.id"
    >
      <span>{{message.name}}</span>
      <i class="material-icons">check_circle</i>
    </div>
    </transition-group>
  </div>
</template>

<script>

  export default {
    name: 'CatalogNotification',
    props: {
      messages: {
        type: Array,
        default() {
          return []
        }
      }
    },
    methods: {
      hideNotification() {
        let vm = this;
        if(!this.messages.length) {
          setInterval(function() {
            vm.messages.splice(vm.messages.length - 1, 1);
          }, 3000);
        }
      }
    },
    mounted() {
      this.hideNotification();
    }
  }
</script>

<style lang="scss" scoped>
  .catalog-notification {
    position: fixed;
    top: 80px;
    right: 16px;
    z-index: 10;
    &__list {
      display: flex;
      flex-direction: column;
    }
    &__content {
      padding: 24px;
      border-radius: 4px;
      color: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 16px;
      margin-bottom: 16px;            
      background-color: rgb(26, 117, 8);
      max-width: 200px;
      text-align: left;
      font-size: 13px;
      &.error {
        background-color: #ff0000;
      }
      &.warning {
        background-color: orange;
      }
      &.check_circle {
        background-color: rgb(26, 117, 8);
      }
    }
    &__content-text {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }
  }
.transition-animate {
  &-enter-from {
    transform: translateX(120px);
    opacity: 0;
  }
  &-enter-active {
    transition: all .6s ease;
  }
  
  &-leave-active {
    transition: transform .6s ease, opacity .6s, height .6s .2s;
  }
  &-leave-to {
    height: 0;
    transform: translateX(120px);
    opacity: 0;
  }
  &-move {
    transition: transform .6s ease;
  }
}
</style>