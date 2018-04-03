<template>
    <div class="wish-list-wrapper">
        <i class="material-icons">playlist_add_check</i>
        <ul class="wish-list">
            <li v-for="wishitem in wishList">
                <span>{{wishitem.name}}</span>
            </li>
        </ul>
    </div>
</template>
<script>
    export default {
        data () {
            return {}
        },
        props: ['wishList']
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