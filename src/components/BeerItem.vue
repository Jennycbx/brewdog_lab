<template>
  <li>{{beer.name}}</li>
</template>

<script>
export default {
    name: 'beer-item',
    props: ['beer']
}
</script>

<style>
li {
    cursor: pointer;
}

li:hover{
    color: red;
}
</style>