<template lang="html">
  <div>
    <h1>PoKéMoN</h1>

    <div>
      <p>First Pokemon:</p>
      <pokemon-filter :pokemons="pokemons" :pokemonsDetails="pokemonsDetails"/>
    </div>

    <div>
      <p>Second Pokemon:</p>
      <pokemon-compare :pokemons="pokemons" :pokemonsDetails="pokemonsDetails"/>
    </div>

    <pokemon-detail/>
  </div>
</template>

<script>
import PokemonFilter from './components/PokemonFilter.vue'
import PokemonDetail from './components/PokemonDetail.vue'
import PokemonCompare from './components/PokemonCompare.vue'

export default {
  name: "app",
  data(){
    return{
      pokemons: [],
      pokemonsDetails: []
    }
  },
  methods: {
    getAllPokemonDetails(){
      for (const pokemon of this.pokemons){
        fetch(pokemon.url)
        .then(res => res.json())
        .then(data => this.pokemonsDetails.push(data))}
      }
    },

    mounted() {
      fetch('https://pokeapi.co/api/v2/pokemon?limit=100&offset=151')
      .then(res => res.json())
      .then(data => {this.pokemons = data['results']
      this.getAllPokemonDetails();}
    )
  },
  components: {
    "pokemon-filter": PokemonFilter,
    "pokemon-detail": PokemonDetail,
    "pokemon-compare": PokemonCompare
  }
}
</script>


<style lang="css" scoped>

</style>
