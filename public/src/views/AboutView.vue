<script>
import Header from '../components/Header.vue'

export default {
  props: ['basket', 'addToBasket'],
  components: { Header }
}
</script>

<template>
  <div>
    <Header :basket="basket" />
    <section class="about-us">
      <h1 class="image">О нас</h1>
      <div class="content">
        <p class="image">
          Добро пожаловать в наш магазин органического стекла! Мы гордимся тем, что предлагаем высококачественное органическое стекло как в оптовой, так и в розничной продаже. Наша миссия - предоставить клиентам продукцию, сочетающую в себе качество, экологичность и инновации.
        </p>
        <p class="image">
          Наш магазин основан на принципах устойчивого развития и заботы об окружающей среде. Мы верим, что органическое стекло является отличной альтернативой традиционным материалам, предлагая не только превосходные эксплуатационные характеристики, но и минимизируя вредное воздействие на природу.
        </p>
      </div>
    </section>
  </div>
</template>

<style scoped>
.about-us {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.about-us h1 {
  font-size: 36px;
  margin-top: 50px;
  font-weight: 700;
  text-align: center;
}

.about-us .content {
  font-size: 18px;
  line-height: 1.6;
  margin-top: 20px;
}

.about-us p {
  margin: 20px 0;
}
</style>
