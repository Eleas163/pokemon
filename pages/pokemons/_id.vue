<template>
  <div class="container py-5">
    <NuxtLink to="/">Go Back</NuxtLink>
    <div v-if="pokemon.sprites" class="hero-container">
      <img :src="pokemon.sprites.front_default" alt="" class="image" />
      <div class="info-box">
        <h1>{{ pokemon.name }}</h1>
        <ul class="list-group mt-5">
          <li class="list-group-item">Weight: {{ pokemon.weight }}</li>
          <li class="list-group-item">
            Base Experience: {{ pokemon.base_experience }}
          </li>
          <li class="list-group-item">Height: {{ pokemon.height }}</li>
        </ul>
      </div>
    </div>
    <div class="whats-included-container">
      <div class="row">
        <div class="col">
          <div class="included-container">
            <h1>Abilities</h1>
            <ul
              class="list-group"
              v-for="ability in pokemon.abilities"
              :key="ability.slot"
            >
              <li class="list-group-item">{{ ability.ability.name }}</li>
            </ul>
          </div>
          <div class="included-container">
            <h1>Forms</h1>
            <ul class="list-group" v-for="form in pokemon.forms" :key="form">
              <li class="list-group-item">{{ form.name }}</li>
            </ul>
          </div>
          <div class="included-container">
            <h1>Game Indices</h1>
            <ul
              class="list-group"
              v-for="game in pokemon.game_indices"
              :key="game"
            >
              <li class="list-group-item">
                Game Index{{ game.game_index }} || Name: {{ game.version.name }}
              </li>
            </ul>
          </div>
          <div class="included-container">
            <h1>Stats</h1>
            <ul class="list-group" v-for="stat in pokemon.stats" :key="stat">
              <li class="list-group-item">
                Name: {{ stat.stat.name }} || Base Stat: {{ stat.base_stat }} ||
                Effort: {{ stat.effort }}
              </li>
            </ul>
          </div>
          <div class="included-container">
            <h1>Types</h1>
            <ul
              class="list-group"
              v-for="type in pokemon.types"
              :key="type.slot"
            >
              <li class="list-group-item">
                Slot: {{ type.slot }} || Name: {{ type.type.name }}
              </li>
            </ul>
          </div>
        </div>
        <div class="col">
          <div class="included-container">
            <h1>Moves</h1>
            <ul class="list-group" v-for="move in pokemon.moves" :key="move">
              <li class="list-group-item">
                {{ move.move.name }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <div class="description-container">
      <p></p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemon: {}
    };
  },
  async fetch() {
    this.pokemon = await fetch(
      `https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`
    ).then(res => res.json());
  }
};
</script>

<style scoped>
.hero-container {
  display: flex;
  justify-content: space-between;
}
.image {
  height: 25rem;
}
.info-box {
  width: 39%;
  background-color: rgba(207, 201, 201, 0.322);
  padding: 1rem;
  border-radius: 0.5rem;
}
.whats-included-container {
  border-bottom: 0.1rem solid rgba(128, 128, 128, 0.151);
}
.description-container {
  border-bottom: 0.1rem solid rgba(128, 128, 128, 0.151);
  padding-bottom: 2rem;
  margin-bottom: 2rem;
}
.included-container {
  margin-top: 1.5rem;
}
h1 {
  font-size: 1.75rem;
}
h6 {
  font-size: 1.15rem;
  font-weight: 400;
}
p {
  color: grey;
}
.snippet {
  color: rgba(0, 0, 0, 0.774);
  margin-top: 1rem;
}
button {
  width: 100%;
  border: none;
  padding: 0.5rem;
  color: white;
  font-weight: 700;
  padding: 1rem 4rem;
  border-radius: 100rem;
  background-color: rgb(231, 81, 43);
  color: white;
  font-weight: 700;
  transition: 0.5s;
}
.description-container {
  margin-top: 3rem;
  color: grey;
}
.padding {
  padding: 10rem 0;
}
</style>
