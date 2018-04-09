<template>
    <div class="main">
        <div class="shop-options">
            <cart-list-component :cartList="cartList"></cart-list-component>
            <wish-list-component :wishList="wishList"></wish-list-component>
        </div>
        <div class="panel-body">
            <div class="list-wrapper">
                <div class="products-list-wrapper">
                    <ul class="products-list">
                        <attributes-list-component :attributesList="attributesList"></attributes-list-component>
                        <product-item-component
                                @addToWish="addToWish"
                                @addToCart="addToCart"
                                @removeProduct="removeProduct"
                                v-for="product in productsList"
                                :key="product.id"
                                :product="product">
                        </product-item-component>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import firebase from 'firebase'
    import config from '../../config/firebase'
    import ProductItemComponent from './ProductItemComponent'
    import AttributesListComponent from './AttributesListComponent'
    import CartListComponent from './CartListComponent'
    import WishListComponent from './WishListComponent'
    firebase.initializeApp(config)
    export default {
        data () {
            return {
                productsList: {},
                attributesList: {},
                wishList: [],
                cartList: []
            }
        },
        created: function () {
            this.getData()
        },
        components: {
            ProductItemComponent,
            AttributesListComponent,
            CartListComponent,
            WishListComponent
        },
        methods: {
            getData: function () {
                let productsListTable = firebase.database().ref('products')
                let attributesIdValueTable = firebase.database().ref('attributesIdValue')
                let attributesTable = firebase.database().ref('attributes')
                let attributesArr = []
                let attributesIdValueArr = []
                let productsListArr = []
                let counterAttr = 0
                attributesTable.once('value', function (snap) {
                    snap.forEach(function (item) {
                        let itemVal = item.val()
                        attributesArr.push(itemVal)
                        counterAttr++
                    })
                })
                this.attributesList = attributesArr
                attributesIdValueTable.once('value', function (snap) {
                    snap.forEach(function (item) {
                        let itemAttrVal = item.val().split('|')
                        attributesIdValueArr.push(itemAttrVal)
                    })
                })
                productsListTable.once('value', function (snap) {
                    snap.forEach(function (item) {
                        let itemVal = item.val()
                        itemVal['informations'] = []
                        for (var i = 0; i < counterAttr; i++) {
                            let attrNames = ''
                            if (itemVal.attributes[i]) {
                                let itemProdVal = itemVal.attributes[i].split('|')
                                itemProdVal.forEach(function (attrItemFor) {
                                    attrNames += attributesIdValueArr[i][attrItemFor - 1] + ' '
                                    itemVal['informations'][i] = attrNames
                                })
                            }
                        }
                        if (i === counterAttr) {
                            let randomArray = (length, max) => [...new Array(length)].map(() => Math.round(Math.random() * max))
                            let newArr = randomArray(4, 9).join('')
                            itemVal['id'] = itemVal.sku + newArr
                        }
                        productsListArr.push(itemVal)
                    })
                })
                this.productsList = productsListArr
            },
            removeProduct: function (idDel) {
                this.productsList = this.productsList.filter(el => el['id'] !== idDel)
            },
            addToCart: function (idCart) {
                let itemCart = this.productsList.filter(el => el['id'] === idCart)
                this.cartList.push(itemCart['0'])
            },
            addToWish: function (idWishlist) {
                let itemWish = this.productsList.filter(el => el['id'] === idWishlist)
                this.wishList.push(itemWish['0'])
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
    ul{
        list-style: none;
    }
    .main{
        width: 100%;
        position: relative;
    }
    .shop-options{
        position: absolute;
        top:40px;
        left: 10px;
        padding: 10px 20px 10px 40px;
        background-color: black;
        opacity: 0.6;
        z-index: 10;
    }
    .shop-options i{
        margin-left: -30px;
    }
    .shop-options ul li:first-child{
        margin-top: -30px;
    }
    .panel-body{
        display: flex;
    }
    .products-list{
        display: flex;
        flex-wrap: wrap;
        padding-left: 150px;
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
    .list-wrapper{
        display: flex;
    }
    .attributes-list li{
        width: 150px
    }
</style>