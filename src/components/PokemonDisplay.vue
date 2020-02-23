<template lang="html">
  <div id="pokemon" v-if="details">
    <section id="top">
      <p>Name: {{details.name}}</p>
      <p>HP: {{getHP}}</p>
    </section>

    <img :src="details.sprites.front_default" height="170" width="200">

    <section id="element">
      <p>ID: {{details.id}}</p>
      <ul>Type:
        <li id="type-li" v-for="type in details.types">{{type.type.name}}</li>
      </ul>
    </section>

    <section>
      <ul id="stats">
        <li id="stats-li" v-for="stats in getStats">{{stats.stat.name}}: {{stats.base_stat}}</li>
      </ul>
    </section>
  </div>
</template>

<script>

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
  props: ["details"]
}
</script>

<style lang="css" scoped>

  img {
    background-color: white;
  }

  #top{
    display: flex;
    justify-content: space-between;
    align-self: stretch;
    margin-top: -15px;
    margin-left: 60px;
    margin-right: 10px;
  }

  #element{
    display: flex;
    justify-content: space-between;
    align-self: stretch;
    margin-top: 10px;
  }

  ul {
    list-style: none;
    display: inline-flex;
  }

  #type-li {
    padding-left: 10px;
  }

  #stats {
    display: inline-flex;
    flex-flow: column;
    justify-content: center;
    padding-right: 70px;
    padding-left: 70px;
    padding-top: 20px;
    padding-bottom: 20px;
    margin-top: -30px;
  }

  #stats-li {
    display: flex;
    justify-content: space-around;
    align-self: center;
  }

</style>
