<script setup>
const query = gql`
  query Pokemons {
    pokemons(orderBy: id_ASC, first: 100) {
      createdAt
      description
      id
      nom
      publishedAt
      slug
      updatedAt
      image {
        url
      }
      types_Pokemons {
        nom
        logo {
          url
        }
      }
    }
  }
`;

const pokemons = ref();
const selectedPokemon = ref(null);
const searchQuery = ref('');

const { data } = await useAsyncQuery(query);
console.log(data.value);
pokemons.value = data.value.pokemons;

onMounted(() => {
  pokemons.value = data.value.pokemons;
});

const showDetails = (pokemon) => {
  selectedPokemon.value = pokemon;
};

const filteredPokemons = computed(() => {
  return pokemons.value.filter((pokemon) =>
    pokemon.nom.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});
</script>

<template>

     <!-- Search input -->
     <input v-model="searchQuery" placeholder="Search for a Pokemon" />

<div class="grid">

  <!-- Liste à gauche -->
  <ul v-if="filteredPokemons" class="pokemon-list">
      <li v-for="pokemon in filteredPokemons" :key="pokemon.id" @mouseover="showDetails(pokemon)">
      <NuxtLink :to="`/pokemon/${pokemon.slug}`">
        <h2 class="text-3xl text-center">{{ pokemon.nom }}</h2>
      </NuxtLink>
    </li>
  </ul>

  <!-- Détails à droite -->
  <div v-if="selectedPokemon" class="details">
      <NuxtImg :src="selectedPokemon.image.url" :alt="selectedPokemon.nom" class="centered-image" />

      <!-- Types du Pokémon -->
      <div class="types">
        <span v-for="(type, index) in selectedPokemon.types_Pokemons" :key="index" class="type">
          <NuxtImg class="type-logo" :src="type.logo.url" :alt="type.nom" />
        </span>
      </div>
  </div>


</div>

</template>

<style scoped>
.grid {
  display: flex;
}

.pokemon-list {
  list-style: none;
  padding: 0;
  margin: 0;
  width: 30%;
  background-color: #f8f8f8;
  border-right: 1px solid #ddd;
}

.pokemon-list li {
  margin-bottom: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.pokemon-list li:hover {
  background-color: #e0e0e0;
}

.details {
  flex: 1;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

.details img {
  width: 40%;
  border: 2px solid #333;
  border-radius: 10px;
}

.details h2 {
  font-size: 2rem;
  margin: 10px 0;
  color: #333;
}

.types {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.type {
  margin-right: 5px;
  margin-bottom: 5px;
  padding: 5px;
  background-color: #ddd;
  border-radius: 5px;
  width: 20%;
  text-align: center;
}

input {
  padding: 8px;
  margin-bottom: 10px;
  width: 100%;
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 14px;
}

.centered-image {
  display: block;
  margin: 0 auto;
}

</style>
