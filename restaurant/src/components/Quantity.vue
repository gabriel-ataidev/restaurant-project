<template>
  <div class="item--quantity">
    <button
      class="buttons"
      @click="decreaseQuantity(item.id)"
      :disabled="item.quantity == 0"
    >
      -
    </button>
    <span class="number">{{ item.quantity }}</span>
    <button class="buttons" @click="increaseQuantity(item.id)">+</button>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  props: {
    item: {},
  },
  methods: {
    ...mapActions(["increaseQuantity", "decreaseQuantity"]),
  },
};
</script>

<style scoped lang="less">
.item--quantity {
  display: flex;
  align-items: center;
  padding-right: 20px;
  .number {
    color: @yellow;
    padding: 10px;
    text-align: center;
  }
  .buttons {
    cursor: pointer;
    font-size: 20px;
    padding: 0;
    background: none;
    border: 0;
    outline: none;
    :focus {
      outline: 0;
    }
  }
}
</style>
