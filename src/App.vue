<template>
  <div id="app">
    <div id="heading">
      <h1><img src="http://assets.stickpng.com/images/585e65d4cb11b227491c3409.png" height="100" width="100" alt="title">Brew Dog Beer</h1>
    </div>

    <div>
      <beers-list :beers="beers"></beers-list>
      <beer-detail :beer="selectedBeer"></beer-detail>
    </div>

    <button class="button" v-if="!favouriteBeer.includes(selectedBeer)" v-on:click="addToFavourite">
      <img src="https://www.brewdog.com/media/catalog/product/cache/eb360c13587b21a8ac6c611a2762b864/p/u/punk_ipa.png" alt="bottle" width="100" height="120">
    </button>
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
body{
  margin-top: 0;
  margin: 0;
}

#app{
  margin: 0;
  background-image: url(https://static.independent.co.uk/s3fs-public/thumbnails/image/2016/11/24/10/brew-dog.jpg);
  height: 100%;
  width: 100%;
  --text-opacity: 1;
  color: #fff;
}
#heading{

  text-align: center;
}

#option-bar{
  margin: 0 auto;
}

.button{
  border: none;
  position: center;
}
</style>