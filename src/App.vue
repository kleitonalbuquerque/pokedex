<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo-pokemon.png" alt="Pokemon Logo" width="50%" />
      <input
        type="text"
        name=""
        id=""
        class="input is-rounded"
        placeholder="Buscar pokemon pelo nome"
        v-model="busca"
      />
      <button
        class="button is-fullwidth is-success"
        id="buscaBtn"
        @click="buscar"
      >
        Buscar
      </button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  components: {
    Pokemon,
  },
  data() {
    return {
      pokemons: [],
      busca: "",
      filteredPokemons: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        // let result = res.data.results;
        // result.push(this.pokemons);
        // console.log(res.data.results);
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.filteredPokemons.filter(
          (pokemon) => pokemon.name == this.busca
        );
      }
    },
  },
  computed: {
    // resultadoBusca: function () {
    //   if (this.busca == "" || this.busca == " ") {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
    //   }
    // },
  },
};
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

#buscaBtn {
  margin-top: 2%;
}
</style>
