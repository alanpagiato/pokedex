<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/alp.png">
      <hr>
      <h4 class="is-size-4">POKEDEX</h4>
      <input type="text" v-model="busca" placeholder="Buscar Pokemon" class="input is-rounded">
      <button class="button is-info is-fullwidth" id="buscarBtn" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
              axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res =>{
                this.pokemons = res.data.results;
                this.filteredPokemons = res.data.results;
                console.log(this.pokemons);
              });
            },

  components: {Pokemon} ,
    
  methods: {
    buscar: function(){
      if(this.busca==''){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name==this.busca);
      }
    }
  },

  computed: {
    /* BUSCA APENAS DIGITANDO NO INPUT
    resultadoBusca: function(){
      if(this.busca==''){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name==this.busca);
      }
    }
    */

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
#buscarBtn{
  margin-top: 2%;
}
</style>
