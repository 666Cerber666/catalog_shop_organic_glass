<template>
    <div class="product-page">
        <div class="item" v-for="el in items" :key="el.slug" @click="goToProduct(el.slug)">
            <img :src="'/img/' + el.image" :alt="el.title" class="photos">
            <h3>{{ el.title }}</h3>
            <p>{{ el.desc }}</p>
            <div class="bottom">
                <span>{{ el.price }} $</span>
                <img src="/img/kosz.png" :alt="el.title" @click="addToBasket(el)">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['slug'],
    data() {
        return {
            product: null
        };
    },
    created() {
        const items = [
            {
                slug: 'item-1',
                image: 'item-1.jpg',
                title: 'Товар 1',
                desc: 'Описание товара 1',
                price: 100
            },
            {
                slug: 'item-2',
                image: 'item-2.jpg',
                title: 'Товар 2',
                desc: 'Описание товара 2',
                price: 200
            },
            {
                slug: 'item-3',
                image: 'item-3.jpg',
                title: 'Товар 3',
                desc: 'Описание товара 3',
                price: 300
            }
        ];

        this.product = items.find(item => item.slug === this.slug);
    },
    methods: {
        addToBasket(product) {
            this.$emit('addToBasket', product);
        }
    }
}
</script>

<style scoped>
.product-page {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    background: #f9f9f9;
    border-radius: 8px;
}
.product-photo {
    width: 100%;
    border-radius: 8px;
}
.product-details {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
}
.price {
    color: #216e5b;
    font-size: 24px;
    font-weight: bold;
}
button {
    padding: 10px 20px;
    background-color: #216e5b;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
button:hover {
    background-color: #1b594a;
}
</style>
