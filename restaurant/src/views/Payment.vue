<template>
  <div class="payment">
    <div class="payment--content">
      <router-link to="/" class="payment--go-back"> ←️ Voltar</router-link>
    </div>
    <Cart v-if="isDesktop()" />
  </div>
</template>

<script>
import Cart from "@/components/Cart.vue";
import Mixin from "@/mixins/mixins";

export default {
  components: {
    Cart,
  },
  mixins: [Mixin],
};
</script>

<style lang="less" scoped>
.payment {
  display: flex;
  &--content {
    flex: 1;
    padding: 50px;
    .payment--go-back {
      font-weight: 600;
      font-size: 20px;
      color: @yellow;
      text-decoration: none;
    }
  }
}
</style>
