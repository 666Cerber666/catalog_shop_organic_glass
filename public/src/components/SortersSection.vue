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
            v-if="accordion.title === 'Цена'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Цена" -->
            {{ accordion.category }}
            <div class="price-filter">
              <div class="wrap-input-price">
                <input v-model.number="minPrice" type="number" :min="0" :max="maxPrice" @input="updateRange">
                <input v-model.number="maxPrice" type="number" :min="minPrice" :max="maxAllowedPrice" @input="updateRange">
              </div>
              <div class="range-input">
                <input v-model.number="minPrice" type="range" :min="0" :max="maxAllowedPrice" @input="updateNumberInputs">
                <input v-model.number="maxPrice" type="range" :min="0" :max="maxAllowedPrice" @input="updateNumberInputs">
              </div>
              <div class="price-display">
                <span>От: {{ minPrice }}</span>
                <span>До: {{ maxPrice }}</span>
              </div>
            </div>
          </div>
          <div
            v-if="accordion.title === 'Бренд'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Бренд" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
          </div>
          <div
            v-if="accordion.title === 'Цвет'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Цвет" -->
            {{ accordion.category }}
            <div><select><option>Все</option><option>Прозрачный</option></select></div>
          </div>
          <div
            v-if="accordion.title === 'Размер'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Размер" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
          </div>
          <div
            v-if="accordion.title === 'Толщина'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Толщина" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
          </div>
          <div
            v-if="accordion.title === 'Плотность'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Плотность" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
          </div>
          <div
            v-if="accordion.title === 'Тип поверхности'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Тип поверхности" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
          </div>
          <div
            v-if="accordion.title === 'Толщина листа'"
            class="accordion-slot"
            @click="openEditor(accordion.category)"
          >
            <!-- Контент для аккордеона "Толщина листа" -->
            {{ accordion.category }}
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
            <div><input type="checkbox"> <label>Bam-bam</label></div>
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
      isEditorOpen: false,
      currentCategory: 'Все',
      minPrice: 0,
      maxPrice: 1000,
      maxAllowedPrice: 1000,
      accordions: [
        { title: 'Цена', category: 'Цена', isOpen: false },
        { title: 'Бренд', category: 'Бренд', isOpen: false },
        { title: 'Цвет', category: 'Цвет', isOpen: false },
        { title: 'Размер', category: 'Размер', isOpen: false },
        { title: 'Толщина', category: 'Толщина', isOpen: false },
        { title: 'Плотность', category: 'Плотность', isOpen: false },
        { title: 'Тип поверхности', category: 'Тип поверхности', isOpen: false },
        { title: 'Толщина листа', category: 'Толщина листа', isOpen: false },
      ],
    };
  },
  methods: {
    toggle(title) {
      this.accordions.forEach((accordion) => {
        if (accordion.title === title) {
          accordion.isOpen = !accordion.isOpen;
        } else {
          accordion.isOpen = false;
        }
      });
    },
    updateRange() {
      if (this.minPrice > this.maxPrice) {
        this.minPrice = this.maxPrice;
      }
    },
    updateNumberInputs() {
      if (this.minPrice > this.maxPrice) {
        this.minPrice = this.maxPrice;
      }
    },
    openEditor(category) {
      this.currentCategory = category;
      this.isEditorOpen = true;
    },
    closeEditor() {
      this.isEditorOpen = false;
    },
    saveCategory() {
      // Логика сохранения измененной категории
      this.closeEditor();
    },
  },
  computed: {
    categories() {
      const categories = this.accordions.map(item => item.category);
      return ['Все', ...new Set(categories)];
    },
  },
};
</script>

<style scoped>
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
  position: absolute;
  z-index: 1;
}
.accordion-slot {
  padding:5px;
  display: flex;
  flex-direction: column;
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
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal-wrapper {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}
.modal-container {
  width: 300px;
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  text-align: center;
}
.modal-footer {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
}
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s;
}
.modal-enter, .modal-leave-to {
  opacity: 0;
}

.wrap-input-price {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.wrap-input-price input {
  width: 48%;
}

.range-input {
  display: flex;
  justify-content: space-between;
}

.range-input input {
  width: 48%;
}

.price-display {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}
</style>
