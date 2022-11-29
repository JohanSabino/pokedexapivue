<template>
  <header>
    <div>
      <h1><img src="../public/titlepokedex.png" /></h1>
      <label for="">
        <img src="../public/pokename.png" />
        <input type="text" v-model="pokemonID" placeholder="bulbasaur or 15" />
        <br />
        <button class="searchButton" @click="searchPokemon">Buscar</button>
      </label>
    </div>
    <main class="main" v-if="Object.entries(pokemonData).length > 0">
      <section class="pokemonCard">
        <div class="nameImage">
          <h1 class="pokemonName">
            {{ pokemonData.name }}
          </h1>
          <img
            :src="pokemonData.sprites.front_default"
            alt="pokemonData.name"
          />
          <ul class="type">
            <h2>Tipo</h2>
            <li v-for="(type, index) in pokemonData.types" :key="index">
              <span> {{ type.type.name }} </span>
            </li>
          </ul>
        </div>

        <ul class="stats">
          <h2>Estadísticas</h2>
          <li
            v-for="(stat, index) in pokemonData.stats"
            :key="index"
            :class="stat.stat.name"
          >
            <span>{{ stat.stat.name }} → {{ stat.base_stat }}</span>
          </li>
        </ul>
      </section>
    </main>
  </header>
</template>

<script>
import { pokeapi } from "@/api/pokeapi";

export default {
  name: "App",
  data() {
    return {
      pokemonData: {},
      pokemonID: "",
    };
  },
  methods: {
    async searchPokemon() {
      try {
        const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`);
        const pokemon = await pokemonToFind.json();
        this.pokemonData = pokemon;
        console.log(pokemon);
        return pokemon;
      } catch (error) {
        alert("Pokemon not found, try in lowercase");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/normalize.css";
@import "@/style.scss";
@import "@/mediaquerie.scss";
@import url("https://fonts.googleapis.com/css2?family=Changa:wght@400;700&display=swap");
</style>
