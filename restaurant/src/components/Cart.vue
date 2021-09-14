<template>
  <div class="cart">
    <h2 class="cart--title">Seu pedido</h2>
    {{cartList}}
  </div>
</template>

<script>
export default {
  name: "Cart",
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
  &--title {
    font-weight: 600;
    font-size: 24px;
  }
}
</style>
