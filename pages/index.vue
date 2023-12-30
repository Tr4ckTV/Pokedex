<script setup>
const query = gql`
  query Pokemons {
    pokemons(orderBy: id_ASC) {
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

<div class="grid">

   <!-- Search input -->
   <input v-model="searchQuery" placeholder="Search for a Pokemon" />

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
      <NuxtImg :src="selectedPokemon.image.url" :alt="selectedPokemon.nom" />
      <h2>{{ selectedPokemon.nom }}</h2>

      <!-- Types du Pokémon -->
      <div class="types">
        <span v-for="(type, index) in selectedPokemon.types_Pokemons" :key="index">
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
}

.pokemon-list li {
  margin-bottom: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.pokemon-list li:hover {
  background-color: #f0f0f0;
}

.details {
  flex: 1;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.details img {
  width: 30%;
  border: 2px solid black;
  border-radius: 10px;
}

.details h2 {
  font-size: 2rem;
  margin: 10px 0;
}

.types {
  display: flex;
  flex-wrap: wrap;
}

.types span {
  margin-right: 5px;
  padding: 5px;
  background-color: #ddd;
  border-radius: 5px;
}


</style>