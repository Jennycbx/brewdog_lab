<template>
    <div>
        <ul>
            <beer-item v-for="(beer, index) in beers" :beer="beer" :key="index"></beer-item>
        </ul>
    </div>
</template>

<script>
import BeerItem from './BeerItem.vue'
export default {
    name: 'beers-list',
    props: ['beers'],
    components: {
        "beer-item": BeerItem
    }
}
</script>

<style>

</style>