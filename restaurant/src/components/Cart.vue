<template>
  <div class="cart">
    <router-link to="/" class="cart--go-back">
      ←️ Continuar comprando</router-link
    >
    <h2 class="cart--title">Seu pedido</h2>
    <div class="cart--content">
      <p v-if="hasNoItem">Seu carrinho ainda está vazio.</p>
      <transition-group name="list">
        <CartItem v-for="item in cartList" :key="item.id" :item="item" />
      </transition-group>
    </div>
      <div class="cart--total" v-if="!hasNoItem">
        <span class="total">Total: </span>
        <span class="price">{{ getCartTotal | currency }}</span>
      </div>
    <button class="primary-button payment-button" @click="goToPayment" v-if="cartList.length">Finalizar pedido</button>
  </div>
</template>

<script>
import CartItem from "./CartItem";
import { mapGetters } from "vuex";
import Mixin from "@/mixins/mixins";
import feather from "feather-icons";

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
    ...mapGetters(["getCartTotal"]),
    cartList() {
      return this.$store.state.cartList;
    },
    hasNoItem() {
      return !this.cartList.length;
    },
    circleIcon() {
      return feather.icons.circle.toSvg();
    },
  },
  methods: {
    goToPayment() {
      this.$router.push({name: 'Payment'});
    }
  }
};
</script>

<style scoped lang="less">
.cart {
  background: #fff;
  width: 643px;
  min-width: 443px;
  padding: 25px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  &--go-back {
    font-weight: 600;
    font-size: 20px;
    color: @yellow;
    text-decoration: none;
    display: none;
  }
  &--title {
    margin-top: 40px;
    font-weight: 600;
    font-size: 24px;
  }
  &--content {
    flex: 1;
    overflow: auto;
  }
    &--total {
      margin: 10px 0 10px auto;
      padding-top: 15px;
      width: fit-content;
      border-top: 1px solid @light-grey;
    }
    .total {
      font-weight: 800;
    }
    .price {
      color: @yellow;
      font-size: 18px;
      font-weight: 800;
    }
  .payment-button {
    margin: 10px auto 0 auto;
    padding: 10px 80px;
  }
  .list-enter-active,
  .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
  }
  @media @small-desktops {
    width: 100%;
    min-width: unset;
    max-width: 800px;
    margin: auto;
    padding: 50px 20px;
    .payment-button {
      margin: auto;
    }
    &--cart-go-back{
      display: block;
    }
  }
}
</style>
