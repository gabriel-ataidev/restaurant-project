<template>
  <div class="item">
      <h2>{{ item.name }}</h2>
      <p>{{ item.description }}</p>
      <p>{{ item.price }}</p>
  </div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: {

        }
    }
}
</script>

<style scoped lang="less">

</style>