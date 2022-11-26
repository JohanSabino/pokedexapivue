<template>
  <header>
    <div>
      <label for="">
        Nombra un Pokemón o da su ID: <br />
        <input type="text" v-model="pokemonID" placeholder="bulbasaur or 15" />
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
        </div>
        <ul class="type">
          <h2>Tipo</h2>
          <li v-for="(type, index) in pokemonData.types" :key="index">
            <span> {{ type.type.name }} </span>
          </li>
        </ul>
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
        alert("Pokemon not found");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style.scss";
@import url("https://fonts.googleapis.com/css2?family=Changa:wght@400;700&display=swap");
template {
  margin: 0;
  padding: 0;
  background-color: #fda2d1;
}
header {
  width: 100%;
  height: 50vh;
}
header div {
  text-align: center;
  width: 100%;
  height: 52px;
  margin-top: 0px;
  align-content: center;
}
label {
  display: block;
  margin: auto;
  width: 60%;
  height: 70px;
  text-align: center;
  background-color: #06c4ce;
  color: #ffdcaa;
  border: 0.5px solid black;
  border-radius: 10px;
  font-size: 1.5rem;
}
label input {
  margin-right: 5px;
}
label button {
  border: 1px solid black;
  border-radius: 15%;
  background-color: #06c4ce;
  color: #ffdcaa;
  transition: 0.3s;
}
label button:hover {
  border: 1px solid black;
  box-shadow: 1px 1px 2px #000000;
  text-shadow: 0px 0px 1px#000000;
  border-radius: 15%;
  background-color: #01c2cc;
  color: #ffdcaa;
}
input[type="text"] {
  border-radius: 10px;
  outline: none;
  border: none;
}
.main {
  margin-left: 10%;
  margin-top: 30px;
  font-size: 1.2rem;
  background-color: $pokedex-green;
  width: 80%;
  height: 300px;
  border-radius: 15px;
  border: 1px solid black;
}
.pokemonCard {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-content: center;
  & .nameImage,
  & .type,
  & .stats {
    width: 33%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }
  & .nameImage {
    & .pokemonName {
      text-transform: capitalize;
    }
    & img {
      width: 200px;
      background-color: #ffbbde;
      border-radius: 35%;
      border: 1px solid black;
      transition: 0.5s;
    }
    & img:hover {
      width: 200px;
      background-color: #fc93c9;
      border-radius: 35%;
      border: 2px solid black;
      box-shadow: 2px 3px 5px black;
    }
  }
  & .type li {
    width: 90%;
    margin-bottom: 10px;
    text-align: center;
    border-radius: 20px;
  }
  & .stats li {
    align-self: flex-start;
  }
}
ul {
  padding: 0;
}
.type {
  & li {
    list-style: none;
    color: rgb(0, 0, 0);
    text-transform: uppercase;
  }
}
.stats {
  color: black;
  & li {
    list-style: none;
    text-transform: uppercase;
  }
}
.color1 {
  color: #ffbbde;
}
.color2 {
  color: #ffdcaa;
}
.color3 {
  color: #0672d1;
}
.color4 {
  color: #06c4ce;
}
.color5 {
  color: #65ffd4;
}
@media screen and (max-width: 900px) {
  .header {
    flex-direction: column;
    height: 120px;
    & .searchButton {
      width: 70%;
      margin-top: 10px;
    }
  }
  .pokemonCard {
    flex-direction: column;
    align-items: center;
    height: 500px;
  }
}
@media screen and (max-width: 300px) {
  .header {
    font-size: 1rem;
    & input[type="text"] {
      font-size: 1rem;
    }
    & .searchButton {
      font-size: 1rem;
    }
  }
  .pokemonCard {
    & .stats {
      width: 90%;
    }
  }
}
@media screen and (max-width: 400px) {
  .header {
    & label {
      text-align: center;
    }
  }
}
</style>
