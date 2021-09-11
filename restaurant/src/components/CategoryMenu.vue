<template>
  <div class="category-menu">
    <ul>
      <li  v-for="category in categoriesList"
                :key="category.id">
        <component :is="category.icon" />
        <p> {{ category.label }} </p>
      </li>
    </ul>
  </div>
</template>

<script>

  import Pizza from '../assets/icons/pizza.svg';
  import Combo from '../assets/icons/french-fries.svg';
  import Deserts from '../assets/icons/ice-cream.svg';
  import Drinks from '../assets/icons/smoothie.svg';
  import Burguer from '../assets/icons/food.svg';

export default {
  name: 'CategoryMenu',
  components: {
    Pizza,
    Combo,
    Deserts,
    Drinks,
    Burguer   
  },
  data() {
    return {
      categoriesList: [
        {label: 'Pizza', icon: 'Pizza', id: 'pizza'},
        {label: 'Bebidas', icon: 'Drinks', id: 'drinks'},
        {label: 'Doces', icon: 'Deserts', id: 'deserts'},
        {label: 'Combos', icon: 'Combo', id: 'combo'},
        {label: 'Burguers', icon: 'Burguer', id: 'burguer'}
      ]
    }
  }
}
</script>
<style lang="less" scoped>

  
</style>