<template>
  <div class="cart">
    <router-link to="/" class="cart--go-back" v-if="isSmallScreens()"> ←️ Continuar comprando</router-link>
    <h2 class="cart--title">Seu pedido</h2>
    <p v-if="hasNoItem">Seu carrinho ainda está vazio.</p>
    <transition-group name="list">
      <CartItem v-for="item in cartList" :key="item.id" :item="item" />
    </transition-group>
    <div class="cart--total" v-if="!hasNoItem">
      <span class="total">Total: </span>
      <span class="price">{{getCartTotal | currency}}</span>
    </div>
  </div>
</template>

<script>
import CartItem from "./CartItem";
import { mapGetters } from 'vuex';
import Mixin from '@/mixins/mixins';
import feather from 'feather-icons';

export default {
  name: "Cart",
  mixins: [Mixin],
  components: {
    CartItem,
  },
  filters: {
    currency(value) {
      return `R$${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })}`;
    },
  },
  computed: {
    ...mapGetters([
      'getCartTotal'
    ]),
    cartList() {
      return this.$store.state.cartList;
    },
    hasNoItem() {
      return !this.cartList.length;
    },
    circleIcon() {
      return feather.icons.circle.toSvg();
    }
  },
};
</script>

<style scoped lang="less">
.cart {
  background: #fff;
  width: 643px;
  min-width: 443px;
  padding: 25px;
  &--go-back{
    font-weight: 600;
    font-size: 20px;
    color: @yellow;
    text-decoration: none;
  }
  &--title {
    margin-top: 40px;
    font-weight: 600;
    font-size: 24px;
  }
  &--total{
    margin-left: auto;
    padding-top: 15px;
    width: fit-content;
    border-top: 1px solid @light-grey;
  }
  .total{
    font-weight: 800;
  }
  .price{
    color: @yellow;
    font-size: 18px;
    font-weight: 800;
  }
  @media @smartphones{
    width: 100%;
    min-width: unset;
    padding: 50px 20px;
  }
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>
