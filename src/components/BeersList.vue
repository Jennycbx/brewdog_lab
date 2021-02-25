<template>
    <form>
        <select v-on:change="handleSelect" v-model='selectedBeer'>
            <option disabled value="">Select a beer</option>
            <option v-for='(beer, index) in beers' :key='index' :value="beer">{{beer.name}}</option>
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
    props: ['beers'],
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

</style>