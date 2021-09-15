<template>
  <div class="cart">
    <router-link to="/" class="cart--go-back"> ←️ Continuar comprando</router-link>
    <h2 class="cart--title">Seu pedido</h2>
    <CartItem v-for="item in cartList" :key="item.id" :item="item" />
  </div>
</template>

<script>
import CartItem from "./CartItem";

export default {
  name: "Cart",
  components: {
    CartItem,
  },
  computed: {
    cartList() {
      return this.$store.state.cartList;
    },
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
  @media @smartphones{
    width: 100%;
    min-width: unset;
    padding: 50px 20px;
    
  }
}
</style>
