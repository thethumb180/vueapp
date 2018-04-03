<template>
    <li>
        <div class="product-panel">
            minicart
        </div>
        <ul class="attributes-list">
            <li v-for="attribute in attributesList">
                <span>{{attribute.name}}</span>
            </li>
        </ul>
    </li>
</template>
<script>
    export default {
        data () {
            return {}
        },
        props: ['attributesList']
    }
</script>

<style scoped>
    ul{
        list-style: none;
    }
    .product-panel{
        padding:10px 3px;
        min-height: 320px;
    }
    .attributes-list{
        width:150px;
    }
</style>