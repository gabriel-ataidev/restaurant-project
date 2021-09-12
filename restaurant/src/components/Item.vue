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

</style>