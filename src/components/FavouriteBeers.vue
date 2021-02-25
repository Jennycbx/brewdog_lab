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
ul {

    list-style: none;
    padding: 0;
}

li {
    display: flex;
    justify-content: center;
    margin: 5px;
}

</style>