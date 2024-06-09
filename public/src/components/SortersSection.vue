<template>
    <div class="wrapper">
      <div
        class="accordion"
        v-for="accordion in accordions"
        :key="accordion.title"
      >
        <div class="accordion-header" @click="toggle(accordion.title)">
          <h2>{{ accordion.title }}</h2>
        </div>
        <transition-group>
          <div
            class="accordion-body"
            v-if="accordion.isOpen"
            key="body"
          >
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
    </div>
  </template>
  
  <script>
  export default {
    props: ['addToBasket', 'items'],
    data() {
      return {
        selectedCategory: 'Все',
        accordions: [
          { title: 'Цена', isOpen: false },
          { title: 'Бренд', isOpen: false },
          { title: 'Цвет', isOpen: false },
          { title: 'Размер', isOpen: false },
          { title: 'Толщина', isOpen: false },
          { title: 'Плотность', isOpen: false },
          { title: 'Тип поверхности', isOpen: false },
          { title: 'Толщина листа', isOpen: false },
        ],
      };
    },
    methods: {
      toggle(title) {
        const accordion = this.accordions.find(a => a.title === title);
        accordion.isOpen = !accordion.isOpen;
      },
    },
    computed: {
      categories() {
        const categories = this.items.map(item => item.category);
        return ['Все', ...new Set(categories)];
      },
    },
  };
  </script>
  
  <style scoped>
  .accordion-header{
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
  </style>
  