<template>
  <div class="cartcontrol">
  <transition name="fade">
    <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart($event)">
       <transition name="inner">
          <span class="inner icon-jian"></span>
        </transition>
    </div>
  </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}} </div>
    <div class="cart-add" @click.stop.prevent="addCart($event)"></div>
  </div>
</template>
<script>
 import Vue from 'vue';
export default {
  props:{
    food:{
      type:Object
    }
  },
  methods:{
    addCart(event){
      if(!event._constructed){
        return;
      }
      if(!this.food.count){
        Vue.set(this.food,'count',1);
      }else{
        this.food.count++;
      }
      this.$emit('increment', event.target);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        // 去掉自带click事件的点击
        return;
      }
      this.food.count--;
    }
  }
}
</script>
<style lang="stylus">
   @import "../../common/stylus/index.styl";
  .cartcontrol
    position:absolute
    right:10px
    bottom:10px
    font-size:0
    .cart-decrease
      display:inline-block
      background:#fff
      padding:6px
      width:18px
      height:18px
      &.fade-enter-active, &.fade-leave-active
        transition: all 0.4s linear
        transform translate3d(0, 0, 0)
      &.fade-enter, &.fade-leave-active
        opacity: 0
        transform translate3d(24px, 0, 0)
      .icon-jian
        width:100%
        height:100%
        display:block
        background:url('remove_circle_outline.png')no-repeat center center
        background-size:18px 18px
        &.inner-enter-active, &.inner-leave-active
          transition: all 0.4s linear
          transform: rotate(0)
        &.inner-enter, &.inner-leave-active
          opacity: 0
          transform:rotate(180deg)
    .cart-count
      display:inline-block
      vertical-align:top
      margin-top:8px
      font-size:14px
    .cart-add
      display:inline-block
      padding:6px
      width:18px
      height:18px
      background:#fff
      background:url('add_circle.png')no-repeat center center
      background-size:18px 18px



</style>
