<template>
  <div>
    <input
      type="text"
      name=""
      id=""
      class="form-control"
      placeholder="Search for a pokemon"
      v-model="search"
    />
    <div class="my-3">
      <ul class="list-group">
        <PokemonCard
          v-for="pokemon in filteredPokemons"
          :key="pokemon.name"
          :pokemon="pokemon"
        />
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemons: [],
      search: ""
    };
  },
  async fetch() {
    let data = await fetch(
      "https://pokeapi.co/api/v2/pokemon?limit=1118"
    ).then(res => res.json());
    this.pokemons = data.results;
  },
  computed: {
    filteredPokemons: function() {
      return this.pokemons.filter(pokemon => {
        return pokemon.name.toLowerCase().match(this.search.toLowerCase());
      });
    }
  }
};
</script>

<style scoped></style>
