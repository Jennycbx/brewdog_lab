<template>
  <div>
      <h2>{{beer.name}}
          <button v-if='favBeers.includes(beer)' v-on:click='handleRemovalClick'>&#127775;</button>
          <button v-if='!favBeers.includes(beer)' v-on:click='handleAddClick'>&#10133;</button>
      </h2>
      <p>ABV: {{beer.abv}}%</p>
      <p>{{beer.description}}</p>
      <div>
          <img :src="beer.image_url" alt="">
          <button>Ingredients List</button>
          <div>
            <p v-for='(malt,index) in beer.ingredients.malt' :key='index'>{{malt.name}}: {{malt.amount.value}} {{malt.amount.unit}}</p>
            <p v-for='(hops,index) in updatedHops' :key='index'>{{hops.name}}: {{hops.amount.value}} {{hops.amount.unit}}</p>
            <p>Yeast: {{beer.ingredients.yeast}}</p>
          </div>
      </div>
      
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'beer-detail',
    data() {
        return {
            updatedHops: []
        }
    },
    props: ['beer', 'favBeers'],
    methods: {
        handleRemovalClick() {
            eventBus.$emit('beer-removal', this.beer)
        },
        handleAddClick() {
            eventBus.$emit('beer-add', this.beer)
        },
        // ingredientDuplicate(hops){
        //     if (this.beer.ingredients.hops.includes(hops)) {
        //         return this.beer.ingredients.hops.reduce((total, hops) => {
        //             total + hops.amount.value
        //         }, 0)
        //     }
        // }
    },
    computed: {
        hopReducer() {
            const hopsData = {}
            this.beer.ingredients.hops.forEach((hops) => {
              if (!hops.name in hopsData) {
                  hopsData[hops.name] = hops 
              } else {
                  hopsData[hops.name].amount.value += hops.amount.value
              }
            })
            this.updatedHops.push(Object.keys(hopsData).map(key => hopsData[key]))
        }
    }
}
</script>

<style>
img {
    height: 200px;
}
</style>