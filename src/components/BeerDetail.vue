<template>
  <div>
    <div v-if="!beer">
      <p>Please Select a Beer</p>
    </div>
    <div v-if="beer" id="beers">
      <h3 class="beers">name: {{beer.name}}</h3>
      <p class="beer-list"> abv: {{beer.abv}}</p>
      <p class="beer-list"> description: {{beer.description}}</p>
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

<style>
.image{
 height: 200px
}
.beers{
 text-align: center;
}

.beer-list{
  display: flex;
  flex-flow: row wrap;
}
</style>