<script>
export default{
    methods: {
        goToProducts() {
            this.$router.push({ name: 'items' });
        }
    },
}
</script>

<template>
<div class="wrapper">
    <aside>
        <h1>Магазин</h1>
        <h2>Органического</h2>
        <h3>Стекла!</h3>
        <p>Органическое стекло оптом и в розницу!</p>
        <button @click="goToProducts()">Что мы предлагаем?</button>
    </aside>
    <img src="../../public/img/photocommercy.png">
</div>
</template>

<style scoped>
.wrapper{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 150px;
}

.wrapper aside{
    margin-left: 50px;
    color: #373845;
}

.wrapper aside h1{
    font-weight: 400;
    font-size: 90px;
}

.wrapper aside h2,
.wrapper aside h3{
    font-weight: 400;
    font-size: 70px;
}

.wrapper aside h3{
    color: #5cb4dd;
}

.wrapper aside p{
    font-size: 18px;
    widows: 500px;
    margin: 20px 0;
}

.wrapper aside button{
    font-weight: 700;
    font-size: 18px;
    color: #2f323a;
    background: #5cb4dd;
    border-radius: 25px;
    border: 0;
    padding: 15px 25px;
    cursor: pointer;
    transition: all 600ms ease;
}

.wrapper aside button:hover{
    transform: translateY(-5px);
}
</style>