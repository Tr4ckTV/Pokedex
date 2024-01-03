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
    pokemonEvolution {
      slug
    }
    attaques {
      nom
      puissance
      type_Attaque {
        nom
        logo {
          url
        }
      }
    }
  }
}
`;


const pokemon = ref();
const pokemonTypes = ref();
const attaques = ref();
const evolution = ref();

const route = useRoute();
const { data, error, loading } = await useAsyncQuery(query, {
  slug: route.params.slug,
});
console.log(data.value);
pokemon.value = data.value.pokemon;
pokemonTypes.value = data.value.types_Pokemons;
attaques.value = data.value.attaques;
evolution.value = data.value.pokemon.pokemonEvolution;
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


    <div v-if="pokemon" class="flex flex-col items-start">
      <NuxtImg class="w-full border-2 border-black rounded-lg" :src="pokemon.image.url" :alt="pokemon.nom" />   

      <div class="p-2 bg-gray-300 rounded-md mt-7">
        <ul>
          <li v-for="(type, index) in pokemon.types_Pokemons" :key="index">
            <NuxtImg
            class="w-20"
            :src="type.logo.url"
            :alt="type.nom"
            />
          </li>
        </ul>
      </div>

    </div>

    <div class="flex flex-col">
      <h2 class="text-2xl m-0">{{ pokemon.nom }}</h2>
      <div v-if="evolution">
        <p class="text-sm italic text-gray-700">Évolution de {{ evolution.slug }}</p>
      </div>
      <p class="mt-10">{{ pokemon.description }}</p>
      <table class="w-full mt-4 border-collapse">
      <thead>
        <tr>
          <th class="border border-black p-2 text-center bg-gray-300">Type</th>
          <th class="border border-black p-2 text-center bg-gray-300">Nom</th>
          <th class="border border-black p-2 text-center bg-gray-300">Puissance</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(attaque, index) in pokemon.attaques" :key="index">
          <td class="border border-black p-2 text-center bg-gray-300">
          <NuxtImg
            class="attaque-logo"
            :src="attaque.type_Attaque.logo.url"
            /></td>
          <td class="border border-black p-2 text-center bg-gray-300">{{ attaque.nom }}</td>
          <td class="border border-black p-2 text-center bg-gray-300">{{ attaque.puissance }}</td>
        </tr>
      </tbody>
    </table>
    </div>


  </div>
</template>


<style scoped>


.pokemon-details-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  display: grid;
  grid-template-columns: 40% 55%; 
  gap: 20px; 
  transform: translateY(20%);
}

.pokemon-attacks {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
}

.pokemon-attacks th,
.pokemon-attacks td {
  border: 1px solid #000000;
  padding: 8px;
  text-align: center;
  background-color: #ddd;
}

.attaque-logo {
  width: 50px;
  margin-left: auto;
  margin-right: auto;
}
</style>

