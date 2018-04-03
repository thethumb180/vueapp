<template>
    <div class="cart-list-wrapper">
        <i class="material-icons">shopping_cart</i>
        <ul class="cart-list">
            <li v-for="cartItem in cartList">
                <span>{{cartItem.name}}</span>
            </li>
        </ul>
    </div>
</template>
<script>
    export default {
        data () {
            return {}
        },
        props: ['cartList']
    }
</script>
<style scoped>
    ul{
        list-style: none;
    }
    .shop-options i{
        margin-left: -30px;
    }
    .shop-options ul li:first-child{
        margin-top: -30px;
    }
</style>