<script setup>
const queryPokemon = gql`
  query Pokemon($slug: String!) {
    pokemon(where: { slug: $slug }) {
      id
      nom
      slug
      description
      createdAt
      image {
        url
      }
      types_pokemons {
        nom
        logo {
          url
        }
      }
    }
  }
`;

const pokemon = ref(null);
const types = ref([]);

const fetchPokemonData = async () => {
  try {
    const route = useRoute();
    console.log("Slug:", route.params.slug);

    const { data, errors } = await useAsyncQuery(queryPokemon, {
      slug: route.params.slug,
    });

    console.log("Data:", data);
    console.log("Errors:", errors); // Ajout de cette ligne

    if (data && data.pokemon) {
      pokemon.value = data.pokemon;
      types.value = data.pokemon.types_pokemons;
    } else {
      console.error("Pokemon not found.");
    }
  } catch (error) {
    console.error("Error fetching Pokemon data:", error);
  }
};

// Appel à la fonction au montage du composant
fetchPokemonData();

const getTypeNames = (types) => {
  return types.map((type) => type.nom).join(", ");
};
</script>

<template>
  <div v-if="pokemon" class="pokemon-details-container">
    <div class="pokemon-header">
      <h2 class="pokemon-name">{{ pokemon.nom }}</h2>
    </div>
    <div class="pokemon-content">
      <div class="pokemon-image">
        <NuxtImg :src="pokemon.image.url" :alt="pokemon.nom" />
        <p class="pokemon-type">Type: {{ getTypeNames(types) }}</p>
      </div>
      <div class="pokemon-info">
        <p class="pokemon-description">{{ pokemon.description }}</p>
      </div>
    </div>
  </div>
  <div v-else>
    <li>Loading...</li>
  </div>
</template>

<style scoped>
.pokemon-details-container {
  max-width: 800px;
  margin: 0 auto;
}

.pokemon-header {
  background-color: #fff;
  padding: 10px;
  border-radius: 8px;
  margin-bottom: 20px;
}

.pokemon-name {
  font-size: 2rem;
  margin: 0;
}

.pokemon-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.pokemon-image {
  width: 40%;
}

.pokemon-info {
  width: 55%;
}

.pokemon-type {
  font-weight: bold;
}
</style>
