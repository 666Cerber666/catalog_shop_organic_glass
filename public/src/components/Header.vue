<script >
export default{
    props: ['basket'],
    data(){
        return{
            showBasket: false,
        }
    },
}
</script>

<template>
    <header>
        <img src="../../public/img/photocommercy.png" class="logo">
        <ul>
            <li><RouterLink to="/" active-class="active">Главная</RouterLink></li>
            <li><RouterLink to="/items" active-class="active">Товары</RouterLink></li>
            <li><RouterLink to="/about" active-class="active">О нас</RouterLink></li>
            <li><img src="/img/purchase.svg" alt="purchase" @click="showBasket = !showBasket"></li>
        </ul>
        <div class="basket" v-if="showBasket">
            <div class="box"></div>
            <h3 v-if="basket.length == 0">У вас еще нет товаров...</h3>
            <div class="items" v-else>
                <div class="item" v-for="el in basket" :key="el.slug">
                    <img :src="'/img/' + el.image" :alt="el.title" class="photos">
                    <h3>{{ el.title }}</h3>
                    <span>{{ el.price }} $</span>
                </div>
                <RouterLink to="/order"><button>Do zamówienia</button></RouterLink>
            </div>
        </div>
    </header>
</template>

<style scoped>
.basket{
    position: absolute;
    top: 50px;
    right: 0;
    padding: 20px;
    width: 250px;
    background: #b2bac1;
    border-radius: 2px;
    z-index: 100;
    box-shadow: 0px 2px 5px 0px rgba(128, 128, 128, 0.4);
}

.basket .box{
    background: #B2BAC1;
    position: absolute;
    top: -7px;
    right: 10px;
    width: 15px;
    height: 15px;
    transform: rotate(45deg);
}

.logo{
    width:50px;
    height:50px;
}

.basket h3{
    color: #65686b;
}

.basket .item{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.basket .item img{
    width: 60px;
}

.basket .item span{
    font-weight: 600;
    color: #323232;
    white-space: nowrap;
}

.basket .item h3{
    color: #52585c;
    text-align: center;
    font-size: 15px;
}


.basket button{
    cursor: pointer;
    width: 100%;
    border: 0;
    height: 50px;
    background: #919191;
    color: #52585c;
    font-weight: 600;
    font-size: 14px;
    transition: all 500ms ease;
}

.basket button:hover{
    background: #757575;
    color: #2f3336;
}

header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 30px;
    position: relative;
}

header ul{
    list-style: none;
}

header ul li{
    display: inline-block;
    margin-left: 25px;
    cursor: pointer;
}

header ul li .active{
    padding: 5px 15px;
    background: #5cb4dd;
    border-radius: 20px;
    transition: all 600ms ease;
}

header ul li .active:hover{
    color: #fff;
    background: #5cb4dd;
}

header ul li a{
    position: relative;
    bottom: 10px;
}
</style>