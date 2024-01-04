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

     <input v-model="searchQuery" placeholder="Search for a Pokemon" />

      <div class="grid">

        <ul v-if="filteredPokemons" class="pokemon-list">
          <li v-for="pokemon in filteredPokemons" :key="pokemon.id" @mouseover="showDetails(pokemon)">
            <NuxtLink :to="`/pokemon/${pokemon.slug}`">
              <h2 class="text-3xl text-center">{{ pokemon.nom }}</h2>
            </NuxtLink>
          </li>
        </ul>

        <div v-if="selectedPokemon" class="details">
          <NuxtImg :src="selectedPokemon.image.url" :alt="selectedPokemon.nom" class="centered-image" />

          <div v-for="(type, index) in selectedPokemon.types_Pokemons" :key="index" class="types">
            <div class="types-container">
              <NuxtImg class="type" :src="type.logo.url" :alt="type.nom" />
            </div>
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
  margin-left: 10%;
  width: 30%;
  background-color: #f8f8f8;
  border-right: 1px solid #ddd;
  margin-right: 20px;
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
  margin-right: 10%;
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
  justify-content:center;
  align-items: center;
}

.types-container {
  display: flex;
  justify-content:center;
  width: 20%;
}

.type {
  padding: 5px;
  background-color: #ddd;
  border-radius: 5px;
  margin-top: 10px;
}

input {
  padding: 8px;
  margin: 0 auto 10px auto;
  width: 80%;
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 14px;
  display: block; 
  margin-left: auto; 
  margin-right: auto; 
}

.centered-image {
  display: block;
  margin: 0 auto;
}

</style>
