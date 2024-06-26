<script>
export default{}
</script>

<template>
<div class="wrapper">
    <div class="topside">
        <h1>Магазин Органического Стекла</h1>
        <h2>Выбирай лучших!</h2>
    </div>
    <div>
        <img src="/img/photocommercy.png" alt="main" class="image">
    </div>
</div>
</template>

<style scoped>
.wrapper{
    background: #3794be;
    width: 104%;
    position: relative;
    right: 13%;
    display: flex;
    padding: 0 12%;
    justify-content: space-between;
    align-items: center;
    height: 240px;
    color: #ffffff;
    margin: 60px 0;
}

.wrapper h1{
    font-size: 70px;
    font-weight: 700;
}

.wrapper h2{
    font-size: 30px;
    font-weight: 400;
    margin-top: 15px;
}

.wrapper img {
    height: 230px;
    position: relative;
    top: 8px;
    right: 30px;
}

@keyframes slideInFromBottom {
            0% {
                transform: translateY(100%);
                opacity: 0;
            }
            100% {
                transform: translateY(0);
                opacity: 1;
            }
        }

.topside{
    animation: 1s ease-out 0s 1 slideInFromBottom;
}

</style>