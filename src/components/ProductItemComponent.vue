<template>
    <li>
        <div class="product-panel">
            <button class="btn-remove" v-bind:data-sku="product.sku" v-on:click="removeProduct(product.sku)">
                <i class="material-icons">close</i>
            </button>
            <div class="row">
                <img v-bind:src="'static/products/' + product.image" alt="">
            </div>
            <div class="row">
                <span class="product-name">{{product.name}}</span>
            </div>
            <div class="row price-wrapper">
                <span v-if="product.price.type === 'special'">
                    <s v-if="product.price.old">{{product.price.old}} PLN </s>{{product.price.value}} PLN
                </span>
                <span v-else>{{product.price.value}} PLN</span>
            </div>
            <button class="btn btn-cart" v-bind:data-sku="product.sku" v-on:click="addToCart(product.sku)">
                koszyk
            </button>
            <button class="btn btn-wishlist" v-bind:data-sku="product.sku" v-on:click="addToWish(product.sku)">
                wishlist
            </button>
        </div>
        <ul>
            <li v-for="item in product.informations">
                {{item}}
            </li>
        </ul>
    </li>
</template>
<script>
export default {
    data () {
        return {
        }
    },
    props: ['product'],
    methods: {
        removeProduct: function (sku) {
            this.$emit('removeProduct', sku)
        },
        addToCart: function (sku) {
            this.$emit('addToCart', sku)
        },
        addToWish: function (sku) {
            this.$emit('addToWish', sku)
        }
    }
}
</script>

<style scoped>
    h1{
        font-size:20px;
    }
    table{
        width:100px;
    }
    .shop-options i{
        margin-left: -30px;
    }
    .shop-options ul li:first-child{
        margin-top: -30px;
    }
    .products-list li{
        padding: 0 10px;
        width: 240px;
        position: relative;
        font-size: 12px;
    }
    .products-list > li:first-child{
        margin-left: -150px;
        width: 150px;
    }
    .products-list > li:first-child .product-panel{
        background-color: transparent;
    }
    ul{
        list-style: none;
    }
    .product-panel{
        padding:10px 3px;
        background-color: black;
    }
    .price-wrapper{
        text-align: center;
        padding: 10px 0;
    }
    .product-name{
        font-size: 14px;
        padding: 5px;
    }
    .product-panel{
        min-height: 320px;
    }
    .btn{
        min-width:38%;
        margin: 0 5%;
        display: inline-block;
        font-size: 12px;
        text-align: center;
    }
    .btn-remove{
        position: absolute;
        top:10px;
        right: 20px;
    }
    .btn-cart{
        background-color: red !important;
    }
    .btn-wishlist{
        background-color: blue !important;
    }
    .attributes-list li{
        width: 150px
    }
</style>