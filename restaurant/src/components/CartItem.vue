<template>
  <div class="item">
    <div class="item--quantity">
      <button class="buttons" @click="decreaseQuantity(item.id)" :disabled="item.quantity == 0">-</button>
      <span class="number">{{ item.quantity }}</span>
      <button class="buttons" @click="increaseQuantity(item.id)">+</button>
    </div>
    <div class="item--img-container">
      <img class="item--img" :src="imagePath" />
    </div>
    <div class="content">
      <h3 class="item--name">{{ item.name }}</h3>
      <a class="item--observation" href="#">adicionar observação</a>
    </div>
    <p class="item--price">{{ item.price | currency }}</p>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: "CartItem",
  props: {
    item: {},
  },
  filters: {
    currency(value) {
      return `R$ ${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })}`;
    },
  },
  computed: {
    imagePath() {
      return require(`../assets/images/${this.item.id}.png`);
    },
  },
  methods: {
    ...mapActions([
      'increaseQuantity',
      'decreaseQuantity'
    ])
  }
};
</script>

<style lang="less" scoped>
.item {
  display: flex;
  margin: 15px 0;
  &--quantity{
    display: flex;
    align-items: center;
    padding-right: 20px;
    .number{
      color: @yellow;
      padding: 10px;
      text-align: center;
    }
    .buttons{
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
  &--img-container {
    background: purple;
    border-radius: 10px;
    background: @light-yellow;
    height: fit-content;
    padding: 4px;
    margin: 0;
    display: flex;
    align-items: center;
    img {
      width: 65px;
      height: 50px;
      margin: auto;
    }
  }
  .content {
    flex-grow: 1;
    padding: 0 10px;
  }
  &--name {
    margin: 0;
    font-size: 18px;
    font-weight: 600;
  }
  &--observation {
    font-weight: 500;
    font-size: 12px;
    color: @dark-grey;
  }
  &--price {
    color: @yellow;
    font-weight: 600;
    line-height: 20px;
    font-size: 18px;
  }
  & + & {
    border-top: 1px solid @light-grey;
    padding-top: 15px;
  }
  @media @tablets{
    flex-wrap: wrap;
    &--img-container{
      order: 1;
    }
    .content{
      order: 2;
    }
    &--quantity{
      order: 3;
      padding-left: 15px;
      padding-right: 100px;
      margin-right: auto;
      justify-content: center;
    }
    &--price{
      order: 4;
      padding-left: 25px;
    }
    & + & {
    padding-top: 30px;
    }
  }
}
</style>
