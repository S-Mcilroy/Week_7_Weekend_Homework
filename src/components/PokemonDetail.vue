<template lang="html">

  <section>

    <div id="pokemon" v-if="pokemon && details">
      <section id="first-pokemon">
        <section id="top">
          <p>Name: {{pokemon.name}}</p>
          <p>HP: {{getHP}}</p>
        </section>

        <img :src="details.sprites.front_default" height="200" width="200">

        <section class= "element">
          <p>ID: {{details.id}}</p>
          <ul>
            <li>Type:</li>
            <li v-for="type in details.types">- {{type.type.name}}</li>
          </ul>
        </section>

        <section class ="element">
          <ul id="stats">
            <li v-for="stats in getStats">{{stats.stat.name}}: {{stats.base_stat}}</li>
          </ul>
        </section>
      </section>
    </div>

    <div id="compared-pokemon" v-if=" comparePokemon && compareDetails">
      <section id="second-pokemon">
        <section id="top">
          <p>Name: {{comparePokemon.name}}</p>
          <p>HP: {{getHPCompare}}</p>
        </section>

        <img :src="compareDetails.sprites.front_default" height="200" width="200">

        <section class= "element">
          <p>ID: {{compareDetails.id}}</p>
          <ul>
            <li>Type:</li>
            <li v-for="type in compareDetails.types">- {{type.type.name}}</li>
          </ul>
        </section>

        <section class ="element">
          <ul id="stats">
            <li v-for="stats in getStatsCompare">{{stats.stat.name}}: {{stats.base_stat}}</li>
          </ul>
        </section>
      </section>
    </div>

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
    }
  },
  mounted(){
    eventBus.$on('pokemon-selected', (pokemon) => {this.pokemon = pokemon});
    eventBus.$on('pokemon-details', (data) => {this.details = data});
    eventBus.$on('pokemon-compare', (pokemon) => {this.comparePokemon = pokemon})
    eventBus.$on('pokemon-compare-details', (data) => {this.compareDetails = data})
  },
  computed: {
    getHP(){
      for (const stats of this.details.stats){
        if (stats.stat.name === 'hp'){
          return stats.base_stat
        }
      }
    },
    getStats(){
      let stats = []
      for (const stat of this.details.stats){
        if (stat.stat.name !== 'hp'){
          stats.push(stat)
        }
      }
      return stats
    },
    getHPCompare(){
      for (const stats of this.compareDetails.stats){
        if (stats.stat.name === 'hp'){
          return stats.base_stat
        }
      }
    },
    getStatsCompare(){
      let stats = []
      for (const stat of this.compareDetails.stats){
        if (stat.stat.name !== 'hp'){
          stats.push(stat)
        }
      }
      return stats
    }
  },
  methods: {

  },
  props:{

  },
  components: {
    "pokemon-display": PokemonDisplay,
  }
}
</script>

<style lang="css" scoped>
#pokemon{
  display: inline-flex;
  flex-flow: column;
  align-items: center;
  position: absolute;
  background-color: Beige;
  left: 35%;
  top: 50%;
  transform: translate(-50%, -50%);
  border: solid black 2px;
  border-radius: 30px;
  padding: 20px;
  width: 300px;
  text-transform: capitalize;
}

#compared-pokemon{
  display: inline-flex;
  flex-flow: column;
  align-items: center;
  position: absolute;
  background-color: Beige;
  left: 65%;
  top: 50%;
  transform: translate(-50%, -50%);
  border: solid black 2px;
  border-radius: 30px;
  padding: 20px;
  width: 300px;
  text-transform: capitalize;
}

img {
  border: solid 2px black;
  border-radius: 50px;
  padding-left: 40px;
  padding-right: 40px;
  background-color: white;
}

#top{
  display: flex;
  justify-content: space-between;
  align-self: stretch;
}

.element{
  display: flex;
  justify-content: space-between;
  align-self: stretch;
}

ul {
  list-style: none;
}

#stats {
  display: inline-flex;
  justify-content: space-between;
}

</style>
