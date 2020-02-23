<template lang="html">
  <div>
    <img src="../public/images/logo.png" height="100" width="300"/>


    <section id="inline">
      <div>
        <p>First Pokemon:</p>
        <pokemon-filter :pokemonsDetails="pokemonsDetails"/>
      </div>

      <div>
        <p>Second Pokemon:</p>
        <pokemon-compare :pokemonsDetails="pokemonsDetails"/>
      </div>
    </section>

    <div id="detail">
      <pokemon-detail/>
    </div>



    <div v-if="chartData" >
      <button v-on:click="hideChart" type="button" name="hideButton">Hide Chart!</button>
      <button v-on:click="showChart" type="button" name="showButton">Show Chart!</button>

      <GChart type="BarChart" :data="chartData" :options="chartOptions" id = "chart"/>
    </div>

  </div>
</template>

<script>
import PokemonFilter from './components/PokemonFilter.vue'
import PokemonDetail from './components/PokemonDetail.vue'
import PokemonCompare from './components/PokemonCompare.vue'
import {eventBus} from './main.js'

export default {
  name: "app",
  data(){
    return{
      pokemons: [],
      pokemonsDetails: [],
      chartData: null,
      chartOptions: {
        'titlePosition': 'none',
        'width': 376,
        'height': 240,
        'fontSize': 15,
        'colors': ['#c87270', '#86dc7e'],
        'chartArea': {
          'width': '80%',
          'height': '100%',
          'left': 120,
          'top': 35,
          'backgroundColor': 'transparent'
        },
        'hAxis': {
          'textStyle': {
            'color': '#2a75bb',
            'bold': 'true',
          }
        },
        'vAxis': {
          'textStyle': {
            'color': '#2a75bb',
            'bold': 'true',
            'italic': 'true',
            'fontSize': 10
          },
          'textPosition': 'out'
        },
        'legend': {
          'position': 'top',
          'textStyle': {
            'color': '#2a75bb',
            'bold': 'true',
            'fontSize': 10
          },
          'alignment': 'left'
        },
        'backgroundColor': 'white'
      }
    }
  },
  methods: {
    getAllPokemonDetails(){
      for (const pokemon of this.pokemons){
        fetch(pokemon.url)
        .then(res => res.json())
        .then(data => this.pokemonsDetails.push(data))}
      },
      hideChart(){
        let chartElement = document.getElementById('chart')
        chartElement.setAttribute("hidden", "")
      },
      showChart(){
        let chartElement = document.getElementById('chart')
        chartElement.removeAttribute("hidden")
      }
    },

    mounted() {
      fetch('https://pokeapi.co/api/v2/pokemon?limit=100&offset=151')
      .then(res => res.json())
      .then(data => {this.pokemons = data['results']
      this.getAllPokemonDetails();
      eventBus.$on('chart-data', (data) => {this.chartData = data})}
    )
  },
  computed: {
  },
  components: {
    "pokemon-filter": PokemonFilter,
    "pokemon-detail": PokemonDetail,
    "pokemon-compare": PokemonCompare
  }
}
</script>

<style lang="css" scoped>

#inline {
  display: inline-flex;
  margin-top: 10px;
}

#chart {
  margin-top: 20px;
  text-transform: uppercase;
  padding-right: 40;
  border: #2a75bb solid 10px;
  z-index: -10;
}

img {
  display: flex;
  justify-content: center;
  padding-left: 30px;
}

p {
  color: white;
}

#detail {
  z-index: 10;
}
</style>
