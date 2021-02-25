<template>
  <div id='app'>
    <h1>Beers</h1>
    <beers-list :beers="beers"></beers-list>
    <beer-detail :beer='selectedBeer'></beer-detail>
    <button v-if="!this.favouriteBeers.includes(this.selectedBeer)" v-on:click='handleClick'>Add to Favourites</button>
    <h2>Favourite Beers</h2>
    <favourite-beers :favBeers='favouriteBeers'></favourite-beers>

  </div>
</template>

<script>
import BeersList from './components/BeersList.vue'
import BeerDetail from './components/BeerDetail.vue'
import FavouriteBeers from './components/FavouriteBeers.vue'

import {eventBus} from './main.js'

export default {
  name: 'App',
  data() {
    return {
      beers: [],
      beers1: [],

      favouriteBeers: [],

      selectedBeer: null
    }
  },

  components: {
    "beers-list": BeersList,
    "beer-detail": BeerDetail,
    "favourite-beers": FavouriteBeers
  },

  mounted() {
    this.fetchBeer()

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer
    })
  },
  methods: {
    fetchBeer: function() {
      fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
        .then(response => response.json())
        .then(data => this.beers = data)
      fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
        .then(response => response.json())
        .then(data => this.beers.push(data))
    },
    handleClick: function() {
      this.favouriteBeers.push(this.selectedBeer)
    }
  },
}
</script>

<style>

</style>