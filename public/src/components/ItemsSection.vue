<script>
import SortersSection from '../components/SortersSection.vue';

export default {
  components: { SortersSection },
  props: ['addToBasket'],
  data() {
    return {
      isOpen: true,
      viewMode: 'grid', // Default view mode
      items: [
        {
          slug: 'item-1',
          image: 'item-1.jpg',
          title: 'Товар 1',
          desc: 'Описание товара 1',
          price: 100,
          category: 'Category 1'
        },
        {
          slug: 'item-2',
          image: 'item-2.jpg',
          title: 'Товар 2',
          desc: 'Описание товара 2',
          price: 200,
          category: 'Category 2'
        },
        {
          slug: 'item-3',
          image: 'item-3.jpg',
          title: 'Товар 3',
          desc: 'Описание товара 3',
          price: 300,
          category: 'Category 1'
        },
        {
          slug: 'item-4',
          image: 'item-4.jpg',
          title: 'Товар 4',
          desc: 'Описание товара 4',
          price: 400,
          category: 'Category 2'
        },
        {
          slug: 'item-5',
          image: 'item-5.jpg',
          title: 'Товар 5',
          desc: 'Описание товара 5',
          price: 500,
          category: 'Category 1'
        }
      ],
      selectedCategory: 'Все'
    };
  },
  methods: {
    goToProduct(slug) {
      this.$router.push({ name: 'product', params: { slug } });
    },
    toggle() {
      this.isOpen = !this.isOpen;
    }
  },
  computed: {
    filteredItems() {
      if (this.selectedCategory === 'Все') {
        return this.items;
      }
      return this.items.filter(item => item.category === this.selectedCategory);
    },
    categories() {
      const categories = this.items.map(item => item.category);
      return ['Все', ...new Set(categories)];
    }
  }
};
</script>


<template>
    <div class="wrapper">
      <div class="accordion">
        <div class="accordion-header" @click="toggle">
          <h2>Категории</h2>
        </div>
        <transition-group>
          <div class="accordion-body" v-if="isOpen">
            <div
              class="accordion-slot"
              v-for="category in categories"
              :key="category"
              @click="selectedCategory = category"
            >
              {{ category }}
            </div>
          </div>
        </transition-group>
      </div>
  
      <div class="wrapper_items">
        <div class="sorters">
          <SortersSection />
        </div>
  
        <div class="view-toggle-icons">
          <i
            class="fas fa-th"
            @click="viewMode = 'grid'"
            :class="{ active: viewMode === 'grid' }"
          ></i>
          <i
            class="fas fa-list"
            @click="viewMode = 'list'"
            :class="{ active: viewMode === 'list' }"
          ></i>
        </div>
  
        <div class="items" :class="viewMode">
          <div
            v-if="viewMode === 'grid'"
            class="item-grid"
            v-for="el in filteredItems"
            :key="el.slug"
            @click="goToProduct(el.slug)"
          >
            <img :src="'/img/' + el.image" :alt="el.title" class="photos image" />
            <h3>{{ el.title }}</h3>
            <p>{{ el.desc }}</p>
            <div class="bottom">
              <span>{{ el.price }} $</span>
              <img
                src="/img/kosz.png"
                class="add_busket"
                :alt="el.title"
                @click.stop="addToBasket(el)"
              />
            </div>
          </div>
  
          <table v-if="viewMode === 'list'" class="item-table">
            <thead>
              <tr>
                <th>Изображение</th>
                <th>Название</th>
                <th>Описание</th>
                <th>Цена</th>
                <th>Добавить в корзину</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="el in filteredItems"
                :key="el.slug"
                @click="goToProduct(el.slug)"
              >
                <td>
                  <img :src="'/img/' + el.image" :alt="el.title" class="photos image" />
                </td>
                <td>{{ el.title }}</td>
                <td>{{ el.desc }}</td>
                <td>{{ el.price }} $</td>
                <td>
                  <img
                    src="/img/kosz.png"
                    class="add_busket"
                    :alt="el.title"
                    @click.stop="addToBasket(el)"
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </template>
  
  

  <style scoped>
.wrapper {
    display: flex;
    gap: 15px;
}

.wrapper_items {
    width: 100%;
}

.sorters {
    display: flex;
    gap: 5px;
}

.category-selector {
    margin-bottom: 20px;
    background-color: #e0f7fa;
    border-radius: 10px;
    text-align: center;
    font-size: 18px;
    display: flex;
    height: 60px;
    cursor: pointer;
    align-items: center;
    justify-content: center;
}

.category-selector label {
    font-weight: bold;
    margin-right: 10px;
}

.category-selector select {
    padding: 10px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    background-color: #ffffff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.category {
    border: 1px solid gray;
    width: 100%;
    height: 80%;
    padding: 10px 0;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
}

.category:hover {
    background: #b6d7db;
}

.ico {
    width: 50px;
    height: 100%;
}

.items {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin-top: 10px;
    gap: 25px;
}

.items.grid .item-grid:hover {
    transform: scale(1.05);
}

.items .item img.photos {
    width: 100%;
}

.items .item h3 {
    margin: 12px 0;
    font-size: 20px;
}

.items .item p {
    margin: 10px 0;
    font-size: 15px;
    width: 90%;
}

.items .item .bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
}

.items .item .bottom span {
    color: #216e5b;
    font-weight: 700;
}

.items.grid .item-grid .bottom img {
    cursor: pointer;
    transition: all 600ms ease;
}

.items .item .bottom img:hover {
    transform: scale(1.2);
}

.add_busket {
    width: 25px;
    height: 25px;
}

i {
    width: 100%;
    height: 100%;
}

.accordion-header {
    background: #f7f7f7;
    padding: 0px 10px;
    height: 60px;
    cursor: pointer;
    border: 1px solid #ddd;
    border-radius: 4px;
    display: flex;
    align-items: center;
}

.accordion-body {
    border: 1px solid #ddd;
    border-radius: 4px;
}

.accordion-slot {
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.accordion-slot:hover {
    height: 50px;
    background: #e0f7fa;
    cursor: pointer;
}

.v-enter-active,
.v-leave-active {
    transition: all 0.5s ease;
}

.v-enter-from,
.v-leave-to {
    transform: translateY(30px);
    opacity: 0;
}

.accordion-slot:nth-child(odd) {
    background-color: #f9f9f9;
}

.accordion-slot:nth-child(even) {
    background-color: #e9e9e9;
}

.accordion-slot:nth-child(even):hover,
.accordion-slot:nth-child(odd):hover {
    background: #e0f7fa;
}

.view-toggle-icons {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 10px;
}

.view-toggle-icons i {
    cursor: pointer;
    width: 50px;
    font-size: 24px;
    margin: 0 10px;
}

.view-toggle-icons .active {
    color: #007bff;
}

.items.list .item-table {
    width: 70%;
    border-collapse: collapse;
}

.items.list .item-table th,
.items.list .item-table td {
    padding: 10px;
    border: 1px solid #ddd;
}
</style>
