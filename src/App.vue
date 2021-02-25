<template>
  <div id='app'>
    <h1>Beers</h1>
    <beers-list :beers="beers" :favBeers='favouriteBeers'></beers-list>
    <beer-detail :beer='selectedBeer' :favBeers='favouriteBeers'></beer-detail>
    <h2 id='fav-beer' v-if='favouriteBeers.length'>Favourite Beers</h2>
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
      const fetch1 = fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
        .then(response => response.json())
      const fetch2 = fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
        .then(response => response.json())
      const fetch3 = fetch('https://api.punkapi.com/v2/beers?page=3&per_page=80')
        .then(response => response.json())
      const fetch4 = fetch('https://api.punkapi.com/v2/beers?page=4&per_page=80')
        .then(response => response.json())
      const fetch5 = fetch('https://api.punkapi.com/v2/beers?page=5&per_page=80')
        .then(response => response.json())
      Promise.all([fetch1, fetch2, fetch3, fetch4, fetch5])
        .then(data => this.beers = (data.flat(1)))
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

<style >
body {
  background-image: url(https://png.pngtree.com/thumb_back/fw800/background/20191116/pngtree-yellow-gradient-beer-bubble-texture-creative-background-image_321722.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  margin: 30px;
}

h1 {
  text-align: center;
}

#fav-beer {
  text-align: center;
}
</style>