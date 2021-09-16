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

<style></style>
