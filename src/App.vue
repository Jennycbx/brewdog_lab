<template>
  <div id='app'>
    <h1>Beers</h1>
    <beers-list :beers="beers" :favBeers='favouriteBeers'></beers-list>
    <beer-detail :beer='selectedBeer' :favBeers='favouriteBeers'></beer-detail>
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

    eventBus.$on('beer-removal', (beer) => {
      this.handleRemovalClick(beer)
    })

    eventBus.$on('beer-add', (beer) => {
      this.handleAddClick(beer)
    })
  },
  methods: {
    fetchBeer: function() {
      fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
        .then(response => response.json())
        .then(data => this.beers = data)
      // fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
      //   .then(response => response.json())
      //   .then(data => this.beers.push(data))
    },
    handleRemovalClick: function(beer) {
      const index = this.favouriteBeers.indexOf(this.selectedBeer)
      this.favouriteBeers.splice(index, 1)
    },
    handleAddClick: function(beer) {
      this.favouriteBeers.push(this.selectedBeer)
    },
  },
}
</script>

<style>

</style>