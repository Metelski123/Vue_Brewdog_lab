<template>
 <div id="option-bar">
   <select id="select" v-on:change='handleSelected' v-model="selectedBeer">
     <option disabled value="">Select beer</option>
     <option v-for="(beer, index) in beers" :value="beer" :key="index">{{beer.name}}</option>
   </select>
 </div>
  
</template>

<script>

import {eventBus} from '../main.js'

export default {
 data(){
   return{
     selectedBeer: {}
   }
 },
 props:['beers'],

 methods: {
  handleSelected() {
    eventBus.$emit('selected-beer', this.selectedBeer)
  }
 }
}
</script>

<style>

#option-bar{
  text-align: center;
}

#select{
  border: 1px gray solid;
  padding: 7px;
  border-radius: 3px;
}

</style>l