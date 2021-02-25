<template>
  <div v-if='beer' class='beer-details'>
      <h2 id='beer-name'>ID. {{beer.id}} {{beer.name}}
          <button v-if='favBeers.includes(beer)' v-on:click='handleRemovalClick'>&#127775;</button>
          <button v-if='!favBeers.includes(beer)' v-on:click='handleAddClick'>&#10133;</button>
      </h2>
      <p id='abv'>ABV: {{beer.abv}}%</p>
      <p id='description'>{{beer.description}}</p>
      <div id='img-section'>
          <img :src="beer.image_url" alt="" id='beer-img'>
          <button v-on:click='ingredientClick' id='ing-but' :class="showIngredients ? 'pressed':'nothing'">Ingredients List</button>
          <div v-if='showIngredients' id='ingredients-list'>
            <p v-for='(malt,index) in beer.ingredients.malt' :key='index'>{{malt.name}}: {{malt.amount.value}} {{malt.amount.unit}}</p>
            <p v-for='(hops,index) in beer.ingredients.hops' :key='index'>{{hops.name}}: {{hops.amount.value}} {{hops.amount.unit}}</p>
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
            updatedHops: [],
            showIngredients: false
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
        ingredientClick() {
            if (!this.showIngredients) {
                this.showIngredients = true
            } else {
                this.showIngredients = false
            }
            
        },
        // ingredientDuplicate(hops){
        //     if (this.beer.ingredients.hops.includes(hops)) {
        //         return this.beer.ingredients.hops.reduce((total, hops) => {
        //             total + hops.amount.value
        //         }, 0)
        //     }
        // }
    },
    // computed: {
    //     hopReducer() {
    //         const hopsData = {}
    //         this.beer.ingredients.hops.forEach((hops) => {
    //             console.log(hopsData)
    //           if (!hops.name in hopsData) {
    //               hopsData[hops.name] = hops 
    //           } else {
    //               hopsData[hops.name].amount.value += hops.amount.value

    //           }
    //         })
    //         this.updatedHops.push(Object.keys(hopsData).map(key => hopsData[key]))
    //     }
    // }
}
</script>

<style>
.beer-details {
    margin: 5px 15%;
}

#beer-name{
    text-align: center;
}

#abv {
    text-align: center;
    color: red;
    font-weight: bold;
}

#description{
    text-align: justify;
    margin: 5px 10%;
}

img {
    height: 300px;
    justify-self: end;
    padding-right: 20px;
}

#img-section {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-areas: "img button"
    "img list";
    justify-items: center;
    margin: 20px 5px;
}

#ing-but {
    height: 150px;
    width: 150px;
    margin-top: 50px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 15px;
}

#ing-but:hover {
    color: red;
    font-weight: bold;
}

#ingredients-list{
    padding-left: 20px;
}

.pressed {
    background-color: rgb(212, 211, 211);
}

</style>