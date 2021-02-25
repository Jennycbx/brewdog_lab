<template>
  <div>
      <h2>{{beer.name}}</h2>
      <p>ABV: {{beer.abv}}%</p>
      <p>{{beer.description}}</p>
      <img :src="beer.image_url" alt="">
  </div>
</template>

<script>
export default {
    name: 'beer-detail',
    props: ['beer']
}
</script>

<style>
img {
    height: 200px;
}
</style>