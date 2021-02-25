<template>
  <div id='app'>
    <h1>Beers</h1>
    <beers-list :beers="beers"></beers-list>
  </div>
</template>

<script>
import BeersList from './components/BeersList.vue'

export default {
  name: 'App',
  data() {
    return {
      beers: [],
      selectedBeer: null
    }
  },

  components: {
    "beers-list": BeersList,
    // "beer-detail": BeerDetail
  },

  mounted() {
    this.fetchBeer()
    // this.fetchNextBeer()
  },
  methods: {
    fetchBeer: function() {
      fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
        .then(response => response.json())
        .then(data => this.beers = data)
    },
    // fetchNextBeer: function() {
    //   fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
    //     .then(response => response.json())
    //     .then(data => this.beers.push(data))
    // }
  }
}
</script>

<style>

</style>