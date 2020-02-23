<template lang="html">

  <section>
    <pokemon-display id="pokemonOne" :details="details"/>
    <pokemon-display id="pokemonTwo" :details="compareDetails"/>
    <button v-if="details && compareDetails" v-on:click=getChartData type="button" name="button">Compare!</button>
  </section>
</template>

<script>
import PokemonDisplay from './PokemonDisplay.vue'
import { eventBus } from '../main.js'

export default {
  name: 'pokemon-detail',
  data(){
    return {
      pokemon: null,
      details: null,
      comparePokemon: null,
      compareDetails: null,
      chartData: [],
    }
  },
  mounted(){
    eventBus.$on('pokemon-details', (data) => {this.details = data});
    eventBus.$on('pokemon-compare-details', (data) => {this.compareDetails = data})
  },
  computed: {
  },
  methods: {
    getChartData(){
      this.chartData = []
      this.chartData.push(["Stats", this.details.name, this.compareDetails.name])
      for (let stat of this.details.stats){
        for (let comparestat of this.compareDetails.stats){
          if (stat.stat.name === comparestat.stat.name){
            this.chartData.push([stat.stat.name, stat.base_stat, comparestat.base_stat])
          }
        }
      }
      eventBus.$emit('chart-data', this.chartData);
    }
  },
  props:{

  },
  components: {
    "pokemon-display": PokemonDisplay,
  }
}
</script>

<style lang="css" scoped>

#pokemonOne{
  display: inline-flex;
  flex-flow: column;
  align-items: center;
  position: absolute;
  background-color: white;
  background-image: url("../../public/images/cardbackground.png");
  background-size: contain;
  background-repeat: no-repeat;
  border-radius: 5%;
  color: white;
  padding: 20px;
  width: 295px;
  text-transform: capitalize;
  margin-top: 50px;
  margin-left: -400px;
  height: 430px;
}

#pokemonTwo{
  display: inline-flex;
  flex-flow: column;
  align-items: center;
  position: absolute;
  background-color: white;
  background-image: url("../../public/images/cardbackground.png");
  background-size: contain;
  background-repeat: no-repeat;
  border-radius: 5%;
  color: white;
  padding: 20px;
  width: 295px;
  text-transform: capitalize;
  margin-left: 450px;
  margin-top: 50px;
  height: 430px;
}

</style>
