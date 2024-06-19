<template>
  <div
    class="container d-flex flex-column justify-content-center align-items-center my-5"
  >
    <img src="../public/pokemon.jpg" alt="logo pokemon" class="m-auto" />
    <h1>¿Quién es ese pokemon?</h1>
    <h5 class="mt-2">Pokemones descubiertos: {{ pokedex }}</h5>
  </div>

  <div class="container my-4">
    <div class="row row-cols-1 row-cols-md-4 g-4">
      <PokemonCard
        v-for="pokemon in pokemones"
        :key="pokemon.nombre"
        :name="pokemon.nombre"
        :image="pokemon.img"
        @nameChecked="handleNameChecked"
      ></PokemonCard>
    </div>
  </div>
</template>

<script>
import PokemonCard from "./components/PokemonCard.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    PokemonCard,
  },
  data() {
    return {
      pokemones: [],
      pokedex: 0,
    };
  },
  mounted() {
    this.getPokemons();
  },
  methods: {
    async getPokemons() {
      try {
        const url = "https://pokeapi.co/api/v2/pokemon?limit=20";
        const { data } = await axios.get(url);
        const pokemons = data.results;
        pokemons.forEach(async (pokemon) => {
          const { data } = await axios.get(pokemon.url);
          const poke = { nombre: data.name, img: data.sprites.front_default };
          this.pokemones.push(poke);
        });
      } catch (error) {
        console.log(error);
      }
    },
    handleNameChecked(acierto) {
      if (acierto) {
        this.pokedex++;
      }
    },
  },
};
</script>

<style></style>
