<script>
import SortersSection from '../components/SortersSection.vue';

export default{
    components: { SortersSection },
    props: ['addToBasket'],
    data(){
        return{
            isOpen: true,
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
        }
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
    },
}
</script>

<template>
    <div class="wrapper">
        <div class="accordion">
            <div class="accordion-header" @click="toggle">
            <h2>Категории</h2>
            </div>
            <transition-group>
                <div class="accordion-body" v-if="isOpen">
                    <div class="accordion-slot" v-for="category in categories" :key="category" @click="selectedCategory = category">
                        {{ category }}
                    </div>
                </div>
            </transition-group>
        </div>
        <div class="wrapper_items">

        <div class="sorters">
            <SortersSection/>
        </div>

        <div class="items">
        <div class="item" v-for="el in filteredItems" :key="el.slug" @click="goToProduct(el.slug)">
            <img :src="'/img/' + el.image" :alt="el.title" class="photos image">
            <h3>{{ el.title }}</h3>
            <p>{{ el.desc }}</p>
            <div class="bottom">
                <span>{{ el.price }} $</span>
                <img src="/img/kosz.png" class="add_busket" :alt="el.title" @click="addToBasket(el)">
            </div>
        </div>
    </div>
    </div>
    </div>
    
</template>

<style scoped>
.wrapper{
    display:flex;
    gap:15px;
}

.wrapper_items{
    width:100%;
}

.sorters{
    display:flex;
    gap:5px;
}

.category-selector {
    margin-bottom: 20px;
    background-color: #e0f7fa; /* Голубой цвет фона */
    border-radius: 10px;
    text-align: center;
    font-size: 18px; /* Увеличение размера текста */
    display:flex;
    height:60px;
    cursor:pointer;
}

.category-selector label {
    font-weight: bold;
    margin-right: 10px;
}

.category-selector select {
    padding: 10px;
    font-size: 16px; /* Увеличение размера текста в селекторе */
    border: none;
    border-radius: 5px;
    background-color: #ffffff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.category{
    border:1px solid gray;
    width:100%;
    height:80%;
    padding:10px 0px 0px 0px;
    text-align: center;
    display:flex;
}

.category:hover{
    background: #b6d7db;
}

.ico{
    width:50px;
    height:100%;
}

.items {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin-top:10px;
    gap:25px;
}

.items .item {
    margin-bottom: 100px;
    width: 350px;
    padding: 15px;
    background: #f4f4f4;
    cursor: pointer;
    transition: transform 0.3s;
}

.items .item:hover {
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

.items .item .bottom img {
    cursor: pointer;
    transition: all 600ms ease;
}

.items .item .bottom img:hover {
    transform: scale(1.2);
}

.add_busket{
    width:25px;
    height:25px;
}

i{
    width:100%;
    height:100%;
}

.accordion-header {
  background: #f7f7f7;
  padding:0px 10px;
  height:60px;
  cursor: pointer;
  border: 1px solid #ddd;
  border-radius: 4px;
  display:flex;
  align-items: center;
}
.accordion-body {
  border: 1px solid #ddd;
  border-radius: 4px;
}
.accordion-slot{
    height:50px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.accordion-slot:hover{
    height:50px;
    background: #e0f7fa;
    cursor:pointer;
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
.accordion-slot:nth-child(even):hover {
    background: #e0f7fa;
}
.accordion-slot:nth-child(odd):hover {
    background: #e0f7fa;
}
</style>