<template>
  <div class="add-cart">
    <router-link to="/" class="add-cart--go-back" v-if="isSmallScreens()">
      ←️ Continuar comprando</router-link
    >
    <Item :item="item" class="add-cart--item" />
    <div class="add-cart--container">
      <span>Quantidade</span>
      <Quantity :item="item" :useStore="false" />
    </div>
      <p class="add-cart--observations">Observações:</p>
      <textarea v-model="item.observations" rows="10"></textarea>
      <button class="primary-button" @click="onAddToCartButtonClick">Adicionar ao carrinho</button>
  </div>
</template>

<script>
import Mixin from "@/mixins/mixins";
import axios from "axios";
import Item from "./Item";
import Quantity from "./Quantity";

export default {
  props: ["id"],
  mixins: [Mixin],
  components: {
    Item,
    Quantity,
  },
  data() {
    return {
      item: {},
    };
  },
  computed: {
    selectedCategory() {
      return this.$store.state.selectedCategory;
    },
  },
  created() {
    axios.get(`http://localhost:3000/${this.selectedCategory}/${this.id}`).then((response) => {
        this.item = { quantity: 1, observations: '', ...response.data}
        // this.item.quantity = 1;
      });
  },
  methods: {
    onAddToCartButtonClick() {
      this.$store.dispatch('addToCart', this.item);
      this.$router.push({name: 'Home'});
    }
  }
};
</script>

<style scoped lang="less">
.add-cart {
  padding: 50px 20px;
  &--go-back {
    font-weight: 600;
    font-size: 20px;
    color: @yellow;
    text-decoration: none;
  }
  &--item{
    margin: 30px 0;
  }
  &--container {
    display: flex;
    background: #fff;
    border: 1px solid @light-grey;
    border-radius: 10px;
    padding: 10px 0 10px 20px;
    margin: 20px 0;
    span{
        margin-right: auto;
        font-weight: 600;
        font-size: 16px;
        margin: auto 0;
        flex: 1;
    }
  }
  &--observations{
      font-weight: 600;
      font-size: 16px;
  }
  textarea{
      width: 100%;
      border-radius: 10px;
      border: 1px solid @light-grey;
      padding: 10px;
      font-size: 16px;
  }
  button{
    width: calc(100% - 40px);
    position: fixed;
    bottom: 30px;
    left: 20px;
    right: 20px;
    cursor: pointer;
  }
}
</style>
