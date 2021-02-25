<template>
<ul>
    <li v-for="beer in favBeers">{{beer.name}}</li>
</ul>
    
  
</template>

<script>
export default {
    name: 'favourite-beers',
    props: ['favBeers'],
   

}
</script>

<style>

</style>