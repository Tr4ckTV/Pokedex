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
        url(
          transformation: {
            image: { resize: { fit: crop, height: 1024, width: 1024 } }
            document: { output: { format: webp } }
          }
        )
      }
    }
    types_Pokemon {
    nom
    logo {
        url(
          transformation: {
            image: { resize: { fit: crop, height: 1024, width: 1024 } }
            document: { output: { format: webp } }
          }
        )
      }
    }
  }
`;

const pokemon = ref();
const types = ref();
const route = useRoute();
const { data } = await useAsyncQuery(query, {
  slug: route.params.slug,
});
console.log(data.value);
pokemon.value = data.value.pokemon;
types.value = data.value.types_Pokemon;
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
            <li v-if="types && types[0]">
              <NuxtImg class="type-logo" :src="types[0].logo.url" :alt="types[0].nom" />
            </li>
            <li v-if="types && types[1]">
              <NuxtImg class="type-logo" :src="types[1].logo.url" :alt="types[1].nom" />
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

.type-logo 
{
  width: 300px; 
  margin-left: 20px; 
}
.pokemon-details-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
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

.pokemon-name {
  font-size: 2rem;
  margin: 0;
}

.pokemon-description {
  margin-top: 10px;
}

/* Ajoutez d'autres styles au besoin */
</style>
