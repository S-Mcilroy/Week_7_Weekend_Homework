<template lang="html">
    <select v-on:change="handleSelect" v-model="selectedPokemon">
      <option disabled value="">Select a pokemon...</option>
      <option v-for="pokemon in pokemonsDetails" :value="pokemon">{{pokemon.name}}</option>
    </select>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "pokemon-filter-form",
  data(){
    return {
      "selectedPokemon": {},
      "detail": {},
    }
  },
  props: ["pokemonsDetails"],
  methods: {
    handleSelect(){
      this.detail = this.pokemonsDetails.filter(detail => detail.name === this.selectedPokemon.name)[0]
      eventBus.$emit('pokemon-compare-details', this.detail)
    }
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
}

select, input[type="text"]{
  font-size: 18px;
}

select {
  margin-left: 20px;
}
</style>
