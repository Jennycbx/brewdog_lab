<template>
    <form>
        <select v-on:change="handleSelect" v-model='selectedBeer'>
            <option disabled value="">Select a beer</option>
            <option v-for='(beer, index) in beers' :key='index' :value="beer">{{beer.name}}
                <span v-if='favBeers.includes(beer)'>&#127775;</span>
            </option>
        </select>
    </form>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'beers-list',
    data(){
        return{
            'selectedBeer': {}
        }
    },
    props: ['beers', 'favBeers'],
    methods: {
        handleSelect() {
            this.search = ""
            eventBus.$emit('beer-selected', this.selectedBeer)
        }
    },
    components: {
    }
}
</script>

<style>
select {
    height: 30px;
}
</style>