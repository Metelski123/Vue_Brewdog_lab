<template lang="html">
  <div id="favourite">
    <h2>Favourite Beers</h2>
      <p v-for="(favouriteBeer, index) in favouriteBeer" :key="index">{{favouriteBeer.name}} <img class="small" :src="favouriteBeer.image_url"></p>
      <button v-on:click="removeBeer">Aye, no thanks pal!</button>
  </div>
</template>

<script>
import BeerListVue from './BeerList.vue'
export default {
  name: 'favourite-beer',
  props: ['favouriteBeer'],

  methods:{
    removeBeer: function(index) {
      return this.favouriteBeer.splice(index, 1)
    }
  }
}
</script>

<style lang="css" scoped>

  #favourite{
    padding: 30px;
    text-align: center;
}

.small{
  height: 100px;
}

</style>