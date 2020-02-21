<template lang="html">
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
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'pokemon-detail',
  data(){
    return {
    }
  },
  mounted(){
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
  },
  methods: {

  },
  props: ["pokemon", "details"]
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
