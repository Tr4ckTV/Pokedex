<script setup>
const query = gql`
query Pokemon($slug: String!) {
  pokemon(where: { slug: $slug }) {
    id
    nom
    slug
    description
    createdAt
    publishedAt
    updatedAt
    stage
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


const pokemon = ref();
const pokemonTypes = ref();
const route = useRoute();
const { data, error, loading } = await useAsyncQuery(query, {
  slug: route.params.slug,
});
console.log(data.value);
pokemon.value = data.value.pokemon;
pokemonTypes.value = data.value.types_Pokemons;

console.log('Pokemon:', pokemon.value);
console.log('Pokemon Types:', pokemonTypes.value);
</script>

<template>
  <div class="pokemon-details-container">
    <Head v-if="pokemon">
      <Title>{{ pokemon.nom }} - Détails du Pokémon</Title>
      <Meta
        name="description"
        :content="`Découvrez des détails sur ${pokemon.nom}: ${pokemon.description}`"
      />
      <Meta
        property="og:title"
        :content="`${pokemon.nom} - Détails du Pokémon`"
      />
      <Meta
        property="og:description"
        :content="`Découvrez des détails sur ${pokemon.nom}: ${pokemon.description}`"
      />
      <Meta property="og:image" :content="pokemon.image.url" />
      <Meta property="og:type" content="website" />
      <Meta property="og:locale" content="fr_FR" />
      <Meta name="twitter:card" content="summary_large_image" />
      <Meta
        name="twitter:title"
        :content="`${pokemon.nom} - Détails du Pokémon`"
      />
      <Meta
        name="twitter:description"
        :content="`Découvrez des détails sur ${pokemon.nom}: ${pokemon.description}`"
      />
      <Meta name="twitter:image" :content="pokemon.image.url" />
    </Head>


    <div v-if="pokemon" class="pokemon-content">
      <NuxtImg class="pokemon-image" :src="pokemon.image.url" :alt="pokemon.nom" />   

      <div class="pokemon-types">
        <ul>
          <li v-for="(type, index) in pokemon.types_Pokemons" :key="index">
            <NuxtImg
            class="type-logo"
            :src="type.logo.url"
            :alt="type.nom"
            />
          </li>
        </ul>
      </div>

    </div>

    <div class="pokemon-info">
      <h2 class="pokemon-name">{{ pokemon.nom }}</h2>
      <p class="pokemon-description">{{ pokemon.description }}</p>
    </div>

  </div>

</template>



<style scoped>
.type-logo {
  width: 100%; /* Ajustez la largeur selon vos besoins */
}

.pokemon-details-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  display: grid;
  grid-template-columns: 40% 55%; /* Définissez les colonnes pour l'image et les informations */
  gap: 20px; /* Ajoutez un espace entre les colonnes */
}

.pokemon-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

/* Style pour l'image Pokémon */
.pokemon-image {
  width: 100%;
  border: 2px solid black;
  border-radius: 10px;
}

/* Style pour la liste des types */
.pokemon-types {
  margin-top: 10px;
}

/* Style pour le logo du type */
.type-logo {
  width: 50px;
  margin-left: 5px;
}

/* Style pour les informations Pokémon */
.pokemon-info {
  display: flex;
  flex-direction: column;
}

/* Style pour le nom Pokémon */
.pokemon-name {
  font-size: 2rem;
  margin: 0;
}

/* Style pour la description Pokémon */
.pokemon-description {
  margin-top: 10px;
}

</style>
