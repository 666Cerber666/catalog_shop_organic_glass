<script>
import Header from '../components/Header.vue'
import HeadSection from '../components/HeadSection.vue';
import ItemSection from '../components/ItemSection.vue';


export default{
  props: ['basket', 'addToBasket'],
  components: { Header, HeadSection, ItemSection }
}

</script>

<template>
  <div>
    <Header :basket="basket"/>
    <HeadSection/>
    <ItemSection :addToBasket="addToBasket"/>
  </div>
</template>
