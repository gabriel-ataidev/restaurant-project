<template>
  <div class="item">
      <div class="item--tag" v-if="item.offer">Oferta</div>
      <img class="item--img" src="../assets/images/burguer.png" alt="burguer">
      <h2 class="item--name">{{ item.name }}</h2>
      <p class="item--description">{{ item.description }}</p>
      <p class="item--price">{{ item.price | currency}}</p>
  </div>
</template>

<script>
export default {
    name: 'Item',
    filters: {
        currency(value) {
            return `R$ ${value.toLocaleString('pt-br', {minimumFractionDigits: 2})}`
        }
    },
    props: {
        item: {

        }
    }
}
</script>

<style scoped lang="less">
.item{
    width: 216px;
    height: fit-content;
    border-radius: 10px;
    background: white;
    position: relative;
    margin: 20px;
    &--tag{
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
    &--img{
        display: block;
        margin: 30px auto;
    }
    img{
        width: 140px;
        height: auto;
    }
    &--name{
        font-weight: 600;
        font-size: 18px;
        margin: 10px;
    }
    &--description{
        color: @dark-grey;
        font-weight: 300;
        font-size: 12px;
        margin: 0 10px;
    }
    &--price{
        font-weight: 600;
        font-size: 18px;
        color: @yellow;
        margin: 0;
        padding: 10px;
    }
}
</style>