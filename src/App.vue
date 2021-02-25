<template>
  <div id="app">
    <div id="heading">
      <h1>Brew Dog Beers</h1>
    </div>

    <div>
      <beers-list :beers="beers"></beers-list>
      <beer-detail :beer="selectedBeer"></beer-detail>
    </div>

    <button class="button" v-if="!favouriteBeer.includes(selectedBeer)" v-on:click="addToFavourite">Add Beer</button>
    <favourite-beer :favouriteBeer="favouriteBeer"></favourite-beer>
  </div>
</template>

<script>

import BeerList from "./components/BeerList.vue";
import BeerDetail from "./components/BeerDetail.vue";
import FavouriteBeer from "./components/FavouriteBeer.vue";

import { eventBus } from './main.js'

export default {
  name: 'app',

  data(){
    return {
    beers: [],
    selectedBeer: null,
    favouriteBeer:[] 
    }
  },
  mounted() {
   fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
     .then(res => res.json())
     .then(data => this.beers = data)

   eventBus.$on('selected-beer', (beer) => {
     this.selectedBeer = beer
   })
  },
  methods:{
    addToFavourite: function () {
    if (!this.selectedBeer) return;
    this.favouriteBeer.push(this.selectedBeer)
    }
  },
  components: {
    "beers-list": BeerList,
    "beer-detail": BeerDetail,
    "favourite-beer": FavouriteBeer
  }
}
</script>

<style>

#app{
  /* background-image:url(//images.ctfassets.net/b0qgo9rl751g/6ktiAGkYidq6y18ed6mEy7/7368b3d49887c5aa6f6eb585c296917e/hp_febrewery_mob.jpg);
  background-image: no-repeat;
  background-color: rgba(0, 0, 0, var(--bg-opacity));
  padding-top: 48px;
  padding-bottom: 48px;
  padding-left: 24px;
  padding-right: 24px;
  --text-opacity: 1;
  color: #fff;
  color: rgba(255, 255, 255, var(--text-opacity)); */
}
#heading{
  text-align: center;
}

#option-bar{
  margin: 0 auto;

}
</style>