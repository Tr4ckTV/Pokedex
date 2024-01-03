<script setup>

const query = gql`
  query Pokemons {
      types_Pokemon {
        nom
        logo {
          url
        }
        forces {
        nom
        logo {
          url
        }
      }
      faiblesses {
        id
        nom
        logo {
          url
        }
      }
      }
  }
`;

const { data } = await useAsyncQuery(query);

const pokemons = ref([]);

console.log(data.value);
pokemons.value = data.value.types_Pokemon;

</script>

<template>
  <div>
    <!-- Types du Pokémon -->
    <table class="types-table">
      <thead>
        <tr>
          <th>Logo</th>
          <th>Fort contre</th>
          <th>Faible contre</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="pokemon in pokemons" :key="pokemon.nom">
          <td><img :src="pokemon.logo.url" alt="Type Logo" class="type-logo" />
            {{ pokemon.nom }}</td>
          <td>
            <ul>
              <li v-for="force in pokemon.forces" :key="force.nom">
                <img :src="force.logo.url" alt="Force Logo" class="type-logo" />
                {{ force.nom }}
              </li>
            </ul>
          </td>
          <td>
            <ul>
              <li v-for="faiblesse in pokemon.faiblesses" :key="faiblesse.id">
                <img :src="faiblesse.logo.url" alt="Faiblesse Logo" class="type-logo" />
                {{ faiblesse.nom }}
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Display loading or error message -->
    <div v-if="fetching">Loading...</div>
    <div v-if="error">{{ error.message }}</div>
  </div>
</template>

<style scoped>
.types-table {
  width: 70%;
  border-collapse: collapse;
  margin-top: 20px;
}

.types-table th, .types-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.type-logo {
  width: 30px; /* Adjust as needed */
  height: auto;
}
</style>