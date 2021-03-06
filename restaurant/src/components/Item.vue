<template>
  <div class="item" @click="addToCart()">
    <div class="container">
      <div class="item--tag" v-if="item.offer">Oferta</div>
      <img class="item--img" :src="imagePath" />
    </div>
    <div class="content">
      <h2 class="item--name">{{ item.name }}</h2>
      <p class="item--description">{{ item.description }}</p>
      <p class="item--price">{{ item.price | currency }}</p>
    </div>
  </div>
</template>

<script>
import Mixin from "@/mixins/mixins";

export default {
  name: "Item",
  mixins: [Mixin],
  filters: {
    currency(value) {
      if (!value) return;
      return `R$ ${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })}`;
    },
  },
  props: {
    item: {},
  },
  computed: {
    imagePath() {
      if (!this.item?.id) return;
      return require(`../assets/images/${this.item.id}.png`);
    },
  },
  methods: {
    addToCart() {
      if (this.isDesktop()) {
        this.$store.dispatch("addToCart", this.item);
        return;
      }

      //if it's mobile
      this.$router.push({ name: "AddToCart", params: { id: this.item.id } });
    },
  },
};
</script>

<style scoped lang="less">
.item {
  width: 216px;
  height: fit-content;
  border-radius: 10px;
  border: 1px solid @light-grey;
  background: white;
  position: relative;
  margin: 20px;
  display: flex;
  flex-direction: column;
  cursor: pointer;
  &--tag {
    position: absolute;
    background: @pink;
    border-radius: 8px;
    color: #fff;
    top: 15px;
    right: 15px;
    font-size: 12px;
    font-weight: 500;
    padding: 3px 8px;
  }
  &--img {
    display: block;
    margin: 25px auto 15px;
    width: 100%;
  }
  img {
    width: 140px;
    height: auto;
  }
  &--name {
    font-weight: 600;
    font-size: 18px;
    margin: 10px;
  }
  &--description {
    color: @dark-grey;
    font-weight: 300;
    font-size: 12px;
    margin: 0 10px;
  }
  &--price {
    font-weight: 600;
    font-size: 18px;
    color: @yellow;
    margin: 0;
    padding: 10px;
  }
  .content {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  @media @smartphones {
    width: 100%;
    height: fit-content;
    border: 1px solid @light-grey;
    display: flex;
    flex-direction: row;
    margin: 5px 10px;
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    &--tag {
      position: static;
      order: 1;
      width: fit-content;
      margin-bottom: 10px;
    }
    &--img {
      order: 0;
      margin: 10px 10px;
    }
    img {
      height: 60px;
      width: auto;
    }
    .content {
      flex-grow: 1;
    }
    &--price {
      text-align: right;
      margin: 0 0 0 auto;
      padding: 5px 10px 10px;
    }
  }
}
</style>
