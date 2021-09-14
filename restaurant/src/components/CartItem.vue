<template>
  <div class="cart-tem">
      <img :src="imagePath">
  </div>
</template>

<script>
export default {
    name: 'CartItem',
    props: {
        item: {}
    },
    computed: {
        selectedCategory() {
            return this.$store.state.selectedCategory;
        },
        imagePath() {
            return require(`../assets/images/${this.selectedCategory}/${this.item.id}.png`)
        }
    }
}
</script>

<style>

</style>