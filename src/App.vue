<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon-logo.png">
      <h4 class="is-size-1">Pokedex</h4>
      <input type="text" v-model="busca" placeholder="Buscar o pokemon pelo nome" class="input is-rounded">
      <button id="btnSearch" class="button is-fullwidth is-success">Buscar</button>
      <div v-for="(poke, index) in search" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      busca: ''
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
    })
  },
  components: {
    Pokemon
  },
  computed: {
    search: function() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons
      } else {
        return this.pokemons.filter(pokemon => !pokemon.name.indexOf(this.busca.toLowerCase()))
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#btnSearch {
  margin-top: 2%;
}
</style>
