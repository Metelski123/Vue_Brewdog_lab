<template>
  <div>
    <div v-if="!beer">
      <p>Please Select a Beer</p>
    </div>
    <div v-if="beer" class="beers">
      <h3>Name: {{beer.name}}</h3>
      <p> Abv: {{beer.abv}}</p>
      <p> Description: {{beer.description}}</p>
      <img class="image" v-bind:src="beer.image_url">
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'beer-detail',
  props: ['beer'],
}
</script>

<style scoped>
.image{
 height: 200px
}

.beers{
  margin: 0 auto;
  width:40%;
}
</style>